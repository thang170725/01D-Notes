- [Mô tả Pipeline Naive RAG](#mô-tả-pipeline-naive-rag)
- [Demo Pipeline Naive RAG + Mistral LLMs](#demo-pipeline-naive-rag--mistral-llms)
---
# Mô tả Pipeline Naive RAG
```bash
Hệ thống hỏi đáp từ tài liệu PDF
Giả sử bạn có: 1 file PDF: “Hướng dẫn sử dụng sản phẩm”
Người dùng hỏi: “Sản phẩm này bảo hành bao lâu?”
```
```bash
1. Load tài liệu:
    - Đưa file pdf vào hệ thống => Lúc này hệ thống chỉ thấy: 1 đống text rất dài (có thể hàng chục trang)
2. Chunking (chia nhỏ):
    - Vì LLM không đọc nổi cả file → bạn phải chia nhỏ
    - Sau khi chunk. Bạn sẽ có dạng:
        Chunk 1: giới thiệu sản phẩm  
        Chunk 2: thông số kỹ thuật  
        Chunk 3: chính sách bảo hành (có câu trả lời)  
        Chunk 4: hướng dẫn sử dụng  
        ...
    - Quan trọng: mỗi chunk = 1 đoạn nhỏ (200–500 tokens), có thể overlap (đè lên nhau một chút)
3. Embedding
    - Mỗi chunk sẽ được biến thành vector (dãy số)
    - Ví dụ: Chunk 3 → [0.12, -0.98, 0.33, ...]
    - Ý nghĩa: vector này đại diện cho “nghĩa” của đoạn text
4. Lưu vào Vector Database
    - Bạn lưu: nội dung chunk, vector của chunk
    - Lúc này hệ thống đã “index xong dữ liệu”
5. User đặt câu hỏi
    - “Sản phẩm bảo hành bao lâu?”
6. Embed câu hỏi
    - Câu hỏi cũng được biến thành vector
    - Query → [0.10, -0.95, 0.30, ...]
7. Retrieve (tìm chunk liên quan)
    - Hệ thống so sánh:
        + vector câu hỏi
        + vector các chunk
    - Nó sẽ tìm ra: Top 3 chunk giống nhất:
        1. Chunk 3 (bảo hành) ✅
        2. Chunk 7 (chính sách đổi trả)
        3. Chunk 2 (thông số kỹ thuật)
    => Đây là bước QUAN TRỌNG NHẤT
8. Tạo context
    - Lấy nội dung của các chunk đó:
    - Context:
        + “Sản phẩm được bảo hành 24 tháng...”
        + “Chính sách đổi trả trong 7 ngày...”
        + ...
9. Nhét vào prompt
    - Hệ thống tạo prompt kiểu:
        Dựa vào thông tin sau:
        [chunk 1]
        [chunk 2]
        [chunk 3]
        Hãy trả lời câu hỏi:
        "Sản phẩm bảo hành bao lâu?"
10. LLM trả lời
    - LLM đọc context → trả lời: “Sản phẩm được bảo hành 24 tháng.”
    - Quan trọng: 
        + LLM KHÔNG tự nghĩ
        + nó chỉ “viết lại” từ context
```
# Demo Pipeline Naive RAG + Mistral LLMs
```python
# ==============================
# STEP 1: IMPORT LIBRARIES
# ==============================

from langchain_community.vectorstores import FAISS
from langchain_community.embeddings import HuggingFaceEmbeddings
from langchain_text_splitters import CharacterTextSplitter
from langchain_ollama import ChatOllama

# ==============================
# STEP 2: LOAD DATA
# ==============================

# Đọc file text (data của bạn)
with open("data.txt", "r", encoding="utf-8") as f:
    raw_text = f.read()

print("\n=== RAW TEXT ===\n", raw_text)


# ==============================
# STEP 3: CHUNKING (PREPROCESSING)
# ==============================

# Chia text thành các đoạn nhỏ (chunk)
# chunk_size: độ dài mỗi đoạn
# chunk_overlap: chồng lấn để giữ context

splitter = CharacterTextSplitter(
    chunk_size=100,
    chunk_overlap=20
)

docs = splitter.split_text(raw_text)

print("\n=== CHUNKS ===")
for i, doc in enumerate(docs):
    print(f"\nChunk {i}:\n{doc}")


# ==============================
# STEP 4: EMBEDDING
# ==============================

# Dùng model embedding local (không cần API)
# model phổ biến: all-MiniLM-L6-v2 (nhẹ, nhanh)

embeddings = HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)


# ==============================
# STEP 5: VECTOR DATABASE (FAISS)
# ==============================

# Convert text chunks -> vector và lưu vào FAISS

vectorstore = FAISS.from_texts(docs, embeddings)

# Tạo retriever để search
retriever = vectorstore.as_retriever(search_kwargs={"k": 2})


# ==============================
# STEP 6: LOAD LLM LOCAL (MISTRAL)
# ==============================

# Kết nối tới Ollama (đang chạy local)
llm = ChatOllama(
    model="mistral",   # tên model trong ollama
    temperature=0
)


# ==============================
# STEP 7: RAG PIPELINE
# ==============================

def rag_pipeline(query):
    print("\n==============================")
    print("USER QUERY:", query)

    # 1. Retrieve docs liên quan
    retrieved_docs = retriever.invoke(query)

    print("\n--- RETRIEVED DOCS ---")
    for doc in retrieved_docs:
        print(doc.page_content)

    # 2. Gộp context
    context = "\n".join([doc.page_content for doc in retrieved_docs])

    # 3. Tạo prompt
    prompt = f"""
Bạn là AI assistant.

Dựa vào context dưới đây để trả lời câu hỏi.
Nếu không có thông tin, hãy nói "Tôi không biết".

Context:
{context}

Question:
{query}

Answer:
"""

    # 4. Gọi LLM
    response = llm.invoke(prompt)

    return response.content


# ==============================
# STEP 8: TEST
# ==============================

if __name__ == "__main__":
    while True:
        query = input("\nNhập câu hỏi (hoặc 'exit'): ")
        if query == "exit":
            break

        answer = rag_pipeline(query)
        print("\n=== FINAL ANSWER ===\n", answer)
```