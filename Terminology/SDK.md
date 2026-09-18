SDK là gì
SDK = Software Development Kit → bộ công cụ dành cho lập trình viên để xây dựng ứng dụng cho một nền tảng/dịch vụ nào đó.

Hiểu đơn giản:

SDK là một “hộp đồ nghề” mà nhà cung cấp đưa cho developer để gọi và sử dụng dịch vụ của họ dễ hơn.

Ví dụ dễ hiểu

Giả sử bạn muốn gọi OpenAI API.

Không có SDK, bạn có thể phải tự gửi HTTP:

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

Có SDK, nhà cung cấp viết sẵn phần HTTP, authentication, serialization... cho bạn:

from some_sdk import Client

client = Client(api_key="xxx")

response = client.chat(
    model="some-model",
    messages=[
        {"role": "user", "content": "Hello"}
    ]
)

Bạn chỉ cần dùng các class, function, method mà SDK cung cấp.

SDK thường chứa những gì?

Một SDK có thể bao gồm:

SDK
├── API Client
├── Authentication
├── Models / Types
├── Helper functions
├── Error handling
├── Serialization
├── Documentation
└── Examples

Ví dụ trong Python:

client.users.get(...)
client.files.upload(...)
client.chat(...)

Những thứ như Client, users, chat, upload()... thường được SDK thiết kế sẵn để bạn không phải tự xử lý HTTP từ đầu.

SDK khác API thế nào?

Đây là chỗ rất quan trọng:

API
= giao diện/quy tắc để phần mềm giao tiếp với nhau

SDK
= bộ công cụ giúp developer sử dụng API đó dễ dàng hơn

Ví dụ:

Your Python App
      │
      ▼
     SDK
      │
      ▼
     API
      │
      ▼
 Server

Bạn có thể dùng API mà không cần SDK.

SDK thường chỉ là lớp tiện ích nằm phía trên API.

SDK, Library, Framework khác nhau

Có thể hiểu sơ bộ:

Khái niệm	Ý nghĩa
API	Quy định cách giao tiếp
SDK	Bộ công cụ để dùng một platform/service
Library	Thư viện code dùng lại
Framework	Khung kiến trúc định hướng cách xây app

Ví dụ trong project AI của bạn:

LangGraph
    ↓
LangChain
    ↓
langchain-ollama
    ↓
Ollama API
    ↓
Ollama
    ↓
Llama/Qwen

Trong đó langchain-ollama có thể xem là integration package/library, giúp LangChain giao tiếp với Ollama; không nên đồng nhất mọi package integration với một "SDK" theo nghĩa chính thức.

Một cách nhớ rất nhanh:

API = cửa giao tiếp
SDK = bộ đồ nghề để đi qua cửa đó
Library = hộp code bạn lấy ra dùng
Framework = bộ khung quy định cách bạn xây nhà.