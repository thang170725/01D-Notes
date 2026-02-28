- [Introduction](#introduction)
---
# Directory Structure
```bash
LangGraph/        # mình dùng thư mục này để xem kiến thức về LangGraph
├── Base.md       # mình dùng file này để xem kiến thức và tiện ích
├── Practices.md  # mình dùng thư mục này để xem code mẫu và bài tập
└── Process.md    # mình dùng thư mục này để thao tác xử lý     
```
# Introduction
```bash
- Nói đơn giản:
    + LangChain → Xây 1 luồng AI chạy từ trên xuống (linear flow)
    + LangGraph → Xây AI như sơ đồ node → node, có thể:
        - Rẽ nhánh
        - Lặp lại
        - Ghi nhớ trạng thái
        - Tạo agent phức tạp
- LangGraph có 3 thứ bạn cần hiểu:
    + State → dữ liệu được truyền giữa các node
    + Node → 1 hàm xử lý trong python
        - Gọi LLM
        - Gọi database
        - Gọi tool
        - Làm bất kỳ logic gì
    + Edge → đường nối giữa các node
```
# Installation
```bash
1. pip install langgraph langchain langchain-community
```
# Work Flow
```bash
START
  ↓
decide
  ↓
(answer simple)  hoặc  (answer detailed)
  ↓
END
```
# Architecture
```bash
ai-assistant/
│
├── app/
│   ├── main.py
│   ├── config.py
│   │
│   ├── graph/
│   │   ├── builder.py
│   │   ├── state.py
│   │   ├── router.py
│   │   └── nodes/
│   │       ├── planner.py
│   │       ├── executor.py
│   │       ├── retriever.py
│   │       ├── tool_node.py
│   │       └── responder.py
│   │
│   ├── llm/
│   │   ├── base.py
│   │   ├── openai_client.py
│   │   └── prompts.py
│   │
│   ├── tools/
│   │   ├── registry.py
│   │   ├── web_search.py
│   │   ├── calculator.py
│   │   └── database_tool.py
│   │
│   ├── memory/
│   │   ├── short_term.py
│   │   ├── long_term.py
│   │   └── vector_store.py
│   │
│   ├── services/
│   │   ├── rag_service.py
│   │   ├── agent_service.py
│   │   └── tool_service.py
│   │
│   └── api/
│       ├── routes.py
│       └── schemas.py
│
├── tests/
├── requirements.txt
└── README.md
```