- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Introduction](#introduction)
- [Installation](#installation)
---
# Cấu trúc thư mục
```bash
LangChain/                  # mình dùng thư mục này để xem kiến thức về langchain
├── Base.md                 # mình dùng file này để xem kiến thức, tiện ích
├── Create_Config_IO.md     # mình dùng file này để khởi tạo, cấu hình, IO
├── Process.md              # mình dùng file này để xem mọi thao tác xử lý trong langchain
├── Results.md              # mình dùng file này để xem mọi thứ mà lanchain trả về
└── Practices.md            # mình dùng file này để xem code mẫu, bài tập
```
# Introduction
```bash
- LangChain = framework để xây dựng hệ thống dùng LLM theo pipeline.
- Nó giúp bạn:
    + Viết prompt có cấu trúc
    + Ghép nhiều bước AI thành pipeline
    + Kết nối AI với:
    + File
    + Database
    + API
    + Tool bên ngoài
- Nếu chỉ gọi OpenAI API → không cần LangChain
- Nếu app có logic, nhiều bước → LangChain rất đáng
```
**LangChain giải quyết vấn đề gì trong dự án thật?**
**Ví dụ KHÔNG dùng LangChain:**
```bash
User → prompt → GPT → text
```
**Ví dụ CÓ LangChain:**
```bash
User
 ↓
PromptTemplate (format chuẩn)
 ↓
LLM
 ↓
Parse output (JSON)
 ↓
Save vào DB / gọi API / chain tiếp

# LangChain giống như:
# “Spring Boot cho LLM” hoặc “Express cho AI”
```
# Cấu trúc
```bash
1. Model (LLM / ChatModel)  # não của hệ thống
2. PromptTemplate           # giúp format dữ liệu
3. OutputParser             # kiểm soát output
4. Runnable (LCEL)          # trái tim kiến trúc mới của langchain (runnable = block có thể chạy được)
5. Memory                   # LLM không có trí nhớ. Memory giúp: Lưu lịch sử hội thoại Inject lại vào prompt
6. Tools                    # Tool = hàm Python mà LLM có thể gọi.
7. Agents                   # Agent = LLM + khả năng quyết định dùng Tool.
8. RAG                      # RAG = cho LLM đọc dữ liệu riêng
9. LangGraph 
```
# Installation
**Trả phí**
```bash
1. pip install langchain langchain-openai
```
**Miến phí**
```bash
1. curl -fsSL https://ollama.com/install.sh | sh
2. ollama pull llama3
3. ollama run llama3
```
