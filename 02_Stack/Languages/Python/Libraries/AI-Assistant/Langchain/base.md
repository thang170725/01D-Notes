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
**Chi tiết**
```bash
2. 02_retrieval.md (Quản lý tri thức - RAG)
Dành cho việc "dạy" LLM đọc dữ liệu của bạn.

Hàm/Class: PyPDFLoader, RecursiveCharacterTextSplitter, Chroma, FAISS, Embeddings.

Mẹo: Nhóm này rất quan trọng cho các dự án "Chat với PDF".

3. 03_chains.md (Sợi dây kết nối)
    + Đây là phần "linh hồn" của LangChain.
    + Nội dung: Tập trung vào LCEL (Sử dụng toán tử | để nối các thành phần).
    + Mẫu tra cứu: chain = prompt | model | parser. Đây là cách viết hiện đại thay thế cho các Chain cũ.

4. 04_memory.md (Trí nhớ cuộc hội thoại)
Hàm/Class: ConversationBufferMemory, ChatMessageHistory.

Mục đích: Giúp chatbot nhớ được những gì người dùng vừa nói ở câu trước.

5. 05_agents_tools.md (Hành động thực tế)
Đây là lúc LLM không chỉ nói mà còn biết làm (Search Google, tính toán, chạy code).

Hàm/Class: initialize_agent, Tool, render_text_description.

Mẹo: Ghi chú cách tạo một Custom Tool để LLM tự gọi hàm Python của bạn.

6. 06_callbacks_tracing.md (Debug & Giám sát)
Hàm/Class: StdOutCallbackHandler, LangChainTracer.

Lý do: Khi Chain bị lỗi hoặc chạy chậm, file này sẽ giúp bạn biết nó đang "tắc" ở đâu.
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