- Cần pip install openai

# Lấy API Key của OpenAI
1. Vào: https://platform.openai.com/
2. Đăng nhập
3. Chọn API Keys
4. Bấm Create new secret key
5. Copy key lại (chỉ thấy 1 lần)

# OpenAI() & .responses.create() & .output_text
```python
from openai import OpenAI
from __init__ import Key

openai_key = Key()

# Khởi tạo client (tự đọc API key từ biến môi trường)
client = OpenAI(api_key=openai_key.get_openai_key())

# Gửi câu hỏi
response = client.responses.create(
    model="gpt-4.1-mini",
    input="Xin chào! Hãy giải thích AI là gì cho người mới học."
)

# In kết quả
print(response.output_text)
```