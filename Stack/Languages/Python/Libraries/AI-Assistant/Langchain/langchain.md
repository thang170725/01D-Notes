-```python
from langchain_community.document_loaders import DirectoryLoader, TextLoader
from langchain_text_splitters import RecursiveCharacterTextSplitter
from langchain_community.vectorstores import FAISS
from langchain_huggingface import HuggingFaceEmbeddings
from langchain_openai import ChatOpenAI
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser
from langchain_core.runnables import RunnablePassthrough
from backend.app.core.__init__ import Key
import os

# Cache để chạy nhanh hơn lần sau
CACHE_PATH = "./cache/faiss_index"

# Load documents
print("📂 Loading documents...")
loader = DirectoryLoader(
    "./backend/app/core", 
    glob="*.py", 
    loader_cls=TextLoader,
    loader_kwargs={"encoding": "utf-8"}, 
    exclude=["**/__init__.py"]
)
documents = loader.load()
print(f"✅ Loaded {len(documents)} files")

# Split với chunk lớn hơn để giữ context
splitter = RecursiveCharacterTextSplitter(
    chunk_size=2000,  # Tăng để giữ nguyên file nhỏ
    chunk_overlap=300,
    separators=["\n\nclass ", "\n\ndef ", "\n\n", "\n"]
)
docs = splitter.split_documents(documents)
print(f"✅ Split into {len(docs)} chunks\n")

# Vector store với cache
if os.path.exists(CACHE_PATH):
    print("📦 Loading from cache...")
    embeddings = HuggingFaceEmbeddings(
        model_name="sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2"
    )
    db = FAISS.load_local(CACHE_PATH, embeddings, allow_dangerous_deserialization=True)
else:
    print("🔨 Creating vector store...")
    embeddings = HuggingFaceEmbeddings(
        model_name="sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2"
    )
    db = FAISS.from_documents(docs, embeddings)
    os.makedirs(os.path.dirname(CACHE_PATH), exist_ok=True)
    db.save_local(CACHE_PATH)
    print("💾 Cached for next run")
print("✅ Vector store ready\n")

# Setup LLM
llm = ChatOpenAI(
    model="gpt-4o-mini",
    temperature=0,
    api_key=Key().get_openai_key(),
    max_tokens=2000
)

# Improved prompt
template = """Bạn là chuyên gia phân tích code Python và bảo mật.

Phân tích CODE THỰC TẾ dưới đây:

{context}

Câu hỏi: {question}

Trả lời CHI TIẾT dựa trên code thực tế:

1. **Chức năng**: File làm gì? Có những class/function nào?
2. **Chi tiết kỹ thuật**: Import gì? Logic ra sao?
3. **Vấn đề bảo mật**: 
   - Input validation có đủ không?
   - Có hardcoded secrets không?
   - Có lỗ hổng nào không? (injection, XSS, etc.)
4. **Đề xuất**: Cải thiện code và bảo mật

Trả lời bằng tiếng Việt, CỤ THỂ và dựa trên CODE:"""

prompt = ChatPromptTemplate.from_template(template)

# Format context với filename
def format_docs(docs):
    result = []
    for doc in docs:
        filename = os.path.basename(doc.metadata['source'])
        result.append(f"=== FILE: {filename} ===\n{doc.page_content}")
    return "\n\n".join(result)

# RAG chain
retriever = db.as_retriever(
    search_type="similarity",
    search_kwargs={"k": 5}  # Lấy nhiều hơn để đảm bảo có test.py
)

chain = (
    {"context": retriever | format_docs, "question": RunnablePassthrough()}
    | prompt | llm | StrOutputParser()
)

# Run analysis
print("🔍 Analyzing...\n")
query = "File test.py đang làm gì? Có vấn đề bảo mật gì không?"

# Debug: Show retrieved docs
print("📚 Retrieved documents:")
retrieved = retriever.invoke(query)
for i, doc in enumerate(retrieved, 1):
    filename = os.path.basename(doc.metadata['source'])
    print(f"   {i}. {filename} ({len(doc.page_content)} chars)")

print("\n" + "="*70)
print("💡 PHÂN TÍCH CHI TIẾT")
print("="*70 + "\n")

result = chain.invoke(query)
print(result)

print("\n" + "="*70)
print("✅ Hoàn tất!")
print("="*70)
```