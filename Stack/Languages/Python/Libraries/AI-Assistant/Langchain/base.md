- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [LangChain là gì \& khi nào nên dùng?](#langchain-là-gì--khi-nào-nên-dùng)
---
# Cấu trúc thư mục
```bash
LangChain/
├── 01_model_io.md           # Nơi tương tác với bộ não
├── 02_retrieval.md          # RAG: DocumentLoaders, TextSplitters, VectorStores
├── 03_chains.md             # Chuỗi xử lý: LCEL (LangChain Expression Language)
├── 04_memory.md             # Bộ nhớ: WindowBuffer, SummaryMemory, DBConn
├── 05_agents_tools.md       # Tác nhân: AgentExecutor, Toolkits, Custom Tools
└── 06_callbacks_tracing.md  # Giám sát: Loggers, LangSmith Integration
```
# LangChain là gì & khi nào nên dùng?
```bash
- LangChain KHÔNG phải là AI. LangChain là framework để điều phối LLM.
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