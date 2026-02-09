- [Sinh tên món ăn](#sinh-tên-món-ăn)
- [Demo AI-driven bằng mistral](#demo-ai-driven-bằng-mistral)
---
# Sinh tên món ăn
```python
import re
from typing import Dict

from langchain_ollama import ChatOllama
from langchain_core.prompts import PromptTemplate


# ========== LLM ==========
llm = ChatOllama(
    model="mistral",
    temperature=0
)


# ========== PROMPTS ==========
dish_prompt = PromptTemplate(
    input_variables=["ingredients"],
    template="""
Chỉ trả về TÊN MỘT MÓN ĂN DUY NHẤT.

Ràng buộc:
- Món phải dùng TẤT CẢ nguyên liệu
- Có thể sử dụng gia vị
- Không giải thích, không mô tả

Nguyên liệu: {ingredients}

Chỉ trả về tên món, 1 dòng.
"""
)

validate_prompt = PromptTemplate(
    input_variables=["dish", "ingredients"],
    template="""
Món ăn: {dish}
Nguyên liệu người dùng có: {ingredients}

Đánh giá mức độ phù hợp của món ăn với các nguyên liệu trên.

Tiêu chí:
- 100: dùng đầy đủ, tự nhiên
- 70–99: dùng đầy đủ nhưng một số nguyên liệu ít phổ biến
- 40–69: dùng được phần lớn
- <40: không phù hợp

QUY TẮC:
- Chỉ trả về MỘT SỐ NGUYÊN từ 0 đến 100
- Không chữ, không giải thích
"""
)


# ========== UTILS ==========
def extract_score(text: str) -> int:
    """
    Không tin LLM.
    Trích số đầu tiên tìm được, fallback = 0
    """
    numbers = re.findall(r"\d+", text)
    if not numbers:
        return 0

    return min(int(numbers[0]), 100)


# ========== CORE LOGIC ==========
def generate_dish_with_score(
    ingredients: str,
    max_retry: int = 3,
    accept_score: int = 80
) -> Dict:
    """
    Luôn trả về kết quả tốt nhất có thể
    """
    best_result = {
        "dish": None,
        "score": 0,
        "status": "fallback"
    }

    for _ in range(max_retry):
        # 1. Generate dish
        dish = llm.invoke(
            dish_prompt.format(ingredients=ingredients)
        ).content.strip()

        # 2. Validate dish
        raw_score = llm.invoke(
            validate_prompt.format(
                dish=dish,
                ingredients=ingredients
            )
        ).content

        score = extract_score(raw_score)

        # 3. Update best result
        if score > best_result["score"]:
            best_result = {
                "dish": dish,
                "score": score,
                "status": "ok" if score >= accept_score else "low_confidence"
            }

        # 4. Early stop
        if score >= accept_score:
            break

    # Absolute fallback (never return None dish)
    if best_result["dish"] is None:
        best_result = {
            "dish": "Món xào tổng hợp",
            "score": 30,
            "status": "rule_based"
        }

    return best_result


# ========== TEST ==========
if __name__ == "__main__":
    result = generate_dish_with_score(
        "thịt heo, hành tây, cà chua, trứng"
    )

    print(result)
```

# Demo AI-driven bằng mistral
```python
from langchain_ollama import ChatOllama
from langchain_core.prompts import PromptTemplate
import json

# ======================
# Fake DB
# ======================
USER_DB = {
    "id": "u1",
    "name": "Nguyen Van A",
    "address": "Da Nang"
}

# ======================
# LLM
# ======================
llm = ChatOllama(
    model="mistral",
    temperature=0
)

prompt = PromptTemplate(
    input_variables=["message"],
    template="""
Bạn là AI backend agent.

Bạn PHẢI quyết định 1 trong các hành động sau và trả về JSON hợp lệ.
KHÔNG giải thích.

Actions:
- GET_USER_INFO
- UPDATE_USER_ADDRESS (requires: address)

Nếu không phù hợp action nào:
{{
  "action": "NONE"
}}

User input:
"{message}"
"""
)

# ======================
# SINGLE ENTRYPOINT
# ======================
def handle_user_input(message: str):
    """
    Đây là HÀM DUY NHẤT được gọi từ bên ngoài
    """
    chain = prompt | llm
    response = chain.invoke({"message": message})

    try:
        decision = json.loads(response.content)
    except Exception:
        raise Exception(f"Invalid JSON:\n{response.content}")

    action = decision.get("action")

    # Router nội bộ (AI quyết định, không phải dev)
    if action == "GET_USER_INFO":
        return USER_DB

    if action == "UPDATE_USER_ADDRESS":
        USER_DB["address"] = decision["address"]
        return USER_DB

    return None

if __name__ == "__main__":
    result = handle_user_input(input())
    print(result)

# tôi muốn xem thông tin tài khoản của tôi
# {'id': 'u1', 'name': 'Nguyen Van A', 'address': 'Da Nang'}
# sửa address thành hà nội cho tôi
# {'id': 'u1', 'name': 'Nguyen Van A', 'address': 'Hà Nội'}
```