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