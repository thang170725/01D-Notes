+ [<<Back](Base.md)
- [SDK (Software Development Kit là bộ công cụ dành cho lập trình viên để xây dựng ứng dụng cho một nền tảng/dịch vụ nào đó)](#sdk-software-development-kit-là-bộ-công-cụ-dành-cho-lập-trình-viên-để-xây-dựng-ứng-dụng-cho-một-nền-tảngdịch-vụ-nào-đó)
---
# SDK (Software Development Kit là bộ công cụ dành cho lập trình viên để xây dựng ứng dụng cho một nền tảng/dịch vụ nào đó)
```bash
SDK là một “hộp đồ nghề” mà nhà cung cấp đưa cho developer để gọi và sử dụng dịch vụ của họ dễ hơn.
```
**Ex: gọi OpenAI API**
**Không có SDK -> bạn có thể phải tự gửi HTTP**
```python
import requests

response = requests.post(
    "https://api.example.com/v1/chat",
    headers={"Authorization": "Bearer xxx"},
    json={
        "model": "some-model",
        "messages": [
            {"role": "user", "content": "Hello"}
        ]
    }
)
```
**Có SDK -> nhà cung cấp viết sẵn phần HTTP, authentication, serialization... cho bạn**
```python
from some_sdk import Client

client = Client(api_key="xxx")

response = client.chat(
    model="some-model",
    messages=[
        {"role": "user", "content": "Hello"}
    ]
)
```
