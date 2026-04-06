- [Sinh tên món ăn](#sinh-tên-món-ăn)
- [Demo AI-driven bằng mistral](#demo-ai-driven-bằng-mistral)
- [Demo một pipeline chuẩn production-style](#demo-một-pipeline-chuẩn-production-style)
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
# Demo một pipeline chuẩn production-style
```bash
1. Router (phân loại READ / ACTION)
2. Read Flow (truy vấn dữ liệu)
3. Action Flow (structured output → validate → confirm → gọi backend giả lập)
4. LCEL chuẩn
5. Tách rõ AI layer và Business layer
-> Sau này bạn có thể dùng khung này để scale lên SaaS / ngân hàng / ecommerce.
```
**Architecture**
```bash
User Input
   ↓
Intent Router (LLM)
   ↓
 ┌───────────────┬────────────────┐
 │               │                │
READ         ACTION            UNKNOWN
 │               │
DB Query     Extract structured data
 │               │
LLM format   Validate → Confirm → Execute
 │               │
Response     Response
```
**Pipeline**
**Step 1: Import & Setup**
```python
from typing import Literal
from pydantic import BaseModel
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser, PydanticOutputParser
from langchain_core.runnables import RunnableLambda, RunnableBranch
```
**Step 2: Model**
```python
model = ChatOpenAI(
    temperature=0
)
```
**Step 3: Intent Router**
```python
class Intent(BaseModel):
    intent: Literal["READ", "ACTION", "UNKNOWN"]

router_parser = PydanticOutputParser(pydantic_object=Intent)

router_prompt = ChatPromptTemplate.from_template("""
Phân loại yêu cầu người dùng thành 1 trong 3 loại:

READ: chỉ xem thông tin
ACTION: thay đổi dữ liệu hệ thống
UNKNOWN: không rõ

User: {input}

{format_instructions}
""")

router_chain = (
    router_prompt.partial(
        format_instructions=router_parser.get_format_instructions()
    )
    | model
    | router_parser
)
```
**Step 4: Read Flow**
```bash
fake_db = {
    "balance": "10,000,000 VND",
    "address": "TP.HCM"
}

def read_account_info(input_dict):
    question = input_dict["input"]

    if "số dư" in question:
        return {"result": fake_db["balance"]}

    if "địa chỉ" in question:
        return {"result": fake_db["address"]}

    return {"result": "Không tìm thấy thông tin"}

read_prompt = ChatPromptTemplate.from_template("""
Dựa vào dữ liệu sau trả lời thân thiện cho người dùng:

Data: {result}
""")

read_chain = (
    RunnableLambda(read_account_info)
    | read_prompt
    | model
    | StrOutputParser()
)
```
**Step 5: Action flow**
```bash
class UpdateAddress(BaseModel):
    action: Literal["update_address"]
    new_address: str

action_parser = PydanticOutputParser(pydantic_object=UpdateAddress)

action_prompt = ChatPromptTemplate.from_template("""
Trích xuất yêu cầu cập nhật địa chỉ.

User: {input}

{format_instructions}
""")

extract_action_chain = (
    action_prompt.partial(
        format_instructions=action_parser.get_format_instructions()
    )
    | model
    | action_parser
)

def execute_action(data: UpdateAddress):
    # Validate
    if len(data.new_address) < 3:
        return "Địa chỉ không hợp lệ"

    # Giả lập update DB
    fake_db["address"] = data.new_address

    return f"Đã cập nhật địa chỉ thành {data.new_address}"

action_chain = (
    extract_action_chain
    | RunnableLambda(execute_action)
)
```
**Step 6: Main Router pipeline**
```bash
def route_logic(input_dict):
    intent = router_chain.invoke(input_dict)

    if intent.intent == "READ":
        return read_chain.invoke(input_dict)

    if intent.intent == "ACTION":
        return action_chain.invoke(input_dict)

    return "Xin lỗi, tôi chưa hiểu yêu cầu."

main_pipeline = RunnableLambda(route_logic)
```