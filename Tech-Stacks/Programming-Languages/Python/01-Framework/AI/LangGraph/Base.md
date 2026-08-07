- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Installation](#installation)
- [Architecture](#architecture)
- [Workflow tổng quan hệ thống AI Agent bằng langgrapgh](#workflow-tổng-quan-hệ-thống-ai-agent-bằng-langgrapgh)
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
```
**LangGraph có 3 thứ bạn cần hiểu**
```bash
State - Chiếc thùng hàng:
  Khi người dùng nhắn 1 câu, hệ thống sẽ tạo ra 1 "thùng hàng". 
    - Thùng này sẽ chạy trên băng chuyền. 
    - Đi qua mỗi trạm, người ta sẽ bỏ thêm đồ vào thùng (thêm tin nhắn, thêm dữ liệu kết quả...).

Node - Các Trạm xử lý
  Đây là các căn phòng trong nhà máy. Thùng hàng chạy vào phòng nào, nhân viên ở phòng đó sẽ làm một nhiệm vụ cụ thể
        - Gọi LLM
        - Gọi database
        - Gọi tool
        - Làm bất kỳ logic gì

Edge / Router (route_...) - Người Bẻ Ghi / Băng Chuyền: 
  Nhiệm vụ của phần này là quyết định xem thùng hàng từ Trạm A sẽ chạy tiếp sang Trạm B, Trạm C, hay chạy ra cửa kết thúc (END).
```
# Installation
```bash
1. pip install langgraph langchain langchain-community
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
# Workflow tổng quan hệ thống AI Agent bằng langgrapgh
```bash
       +---------------------------------------------+
       |                   START                     |
       +---------------------------------------------+
                              |
                              v
       +---------------------------------------------+
       |            Node: retrieve_tools             |  <--- Quét RAG tìm các công cụ 
       |  (Đọc MySQL tìm các tool đọc phù hợp nhất)  |       đáp ứng câu hỏi của user
       +---------------------------------------------+
                              |
                              v
       +---------------------------------------------+
       |               Node: call_llm                |  <--- Đút State["messages"] + Tools
       |       (Gắn Tools và gọi Gemini/LLM)         |       cho LLM. LLM sẽ trả về text
       +---------------------------------------------+       hoặc gọi Tool_Call.
                              |
                              v
                 //=== ROUTE AFTER LLM ===\\
                //                         \\
               //  Hàm route_after_llm()    \\          <--- Bộ định tuyến (Conditional Edge)
              //   kiểm tra kết quả LLM:    \\               đọc cấu trúc phản hồi của LLM
               \\                           //               để bẻ lái luồng đi.
                \\                         //
                 \\=======================//
                    /         |         \
         [no_tool] /          |          \ [read_tool]
                  /           | [write_tool] \
                 v            v               v
       +--------------+ +--------------+ +--------------+
       |  Node:       | |  Node:       | |  Node:       |
       |  handle_chat | |  handle_write| |  handle_read |
       |              | |              | |              |
       | (User chat   | | (Treo action | | (Gọi Tool    |
       |  thông thường| |  vào RAM,    | |  đọc DB, nhờ |
       |  không gọi   | |  LLM sinh câu| |  LLM dịch    |
       |  công cụ)    | |  hỏi xác nhận| |  thành văn   |
       |              | |  cập nhật)   | |  bản)        |
       +--------------+ +--------------+ +--------------+
                 \            |            /
                  \           |           /
                   v          v          v
       +---------------------------------------------+
       |                    END                      |  <--- Kết thúc chu trình của Graph.
       +---------------------------------------------+       Trả State cuối cùng về cho API.
```
```bash
[BẮT ĐẦU - User nhắn tin]
         |
         V
+--------------------------+
| Trạm 1: retrieve_tools   | ---> Lục kho xem có công cụ (tools) nào phù hợp 
+--------------------------+      với câu nói của User không. Bỏ công cụ vào thùng.
         |
         V
+--------------------------+
| Trạm 2: call_llm         | ---> Đưa câu hỏi + công cụ cho não bộ Gemini. 
+--------------------------+      Gemini quyết định xem nên dùng công cụ nào, hay chỉ nói chuyện.
         |
         V
    (Ngã Ba Đường) 
  Hàm: route_after_llm  ---> Bác bảo vệ kiểm tra quyết định của Gemini để bẻ ghi:
         |
  +------+-------+
  |      |       |
Nhánh 1 Nhánh 2 Nhánh 3
  |      |       |
  V      V       V

Chi tiết 3 Nhánh:
  - Nhánh 1 (Không dùng Tool): Chạy vào handle_no_tool_node. Chỉ là chat phiếm -> Trả lời luôn.
  - Nhánh 2 (Dùng Tool Đọc): Chạy vào execute_read_node. Lấy dữ liệu từ Database ra -> Nhờ Gemini dịch thành câu dễ thương -> Trả lời.
  - Nhánh 3 (Dùng Tool Ghi): Chạy vào execute_write_node. Cảnh báo! Việc ghi/sửa dữ liệu là nguy hiểm. Trạm này không sửa luôn mà treo lệnh đó vào một quyển sổ (PENDING_ACTIONS), sau đó nhờ Gemini hỏi lại User: "Bạn có chắc muốn sửa không?"
=> Sau khi chạy xong 1 trong 3 nhánh này, thùng hàng đi ra cửa END và gửi kết quả về cho người dùng.
```