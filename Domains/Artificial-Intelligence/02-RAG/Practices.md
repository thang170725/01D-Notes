# Demo Pipeline RAG + Mistral LLMs
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