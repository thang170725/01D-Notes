Nếu dùng Qdrant với FastAPI (Python) thì thư viện chính thức là:

pip install qdrant-client

Đây là SDK do chính Qdrant phát triển và hỗ trợ cả:

✅ REST API
✅ gRPC (nhanh hơn)
✅ Async
✅ Local mode (chạy trong RAM để test)
✅ Qdrant Cloud
✅ Docker

Đây là thư viện bạn nên dùng trong production.

Bộ thư viện thường dùng
1. Qdrant Client ⭐⭐⭐⭐⭐
pip install qdrant-client

Import

from qdrant_client import QdrantClient

Hoặc async

from qdrant_client import AsyncQdrantClient

Đây là thư viện bắt buộc.

2. Embedding Model

Qdrant không sinh embedding.

Nó chỉ lưu vector.

Bạn phải dùng model embedding.

Ví dụ

Gemini
from google import genai

↓

Text

↓

Embedding

↓

Vector

↓

Qdrant

Hoặc

Sentence Transformers
pip install sentence-transformers
from sentence_transformers import SentenceTransformer

Ví dụ

model = SentenceTransformer("BAAI/bge-m3")

Hoặc

model = SentenceTransformer("all-MiniLM-L6-v2")

Hoặc

OpenAI Embedding

client.embeddings.create(...)
3. FastAPI
pip install fastapi
4. SQLAlchemy

Nếu kết hợp SQL

pip install sqlalchemy
5. Async Driver

Ví dụ PostgreSQL

pip install asyncpg

MariaDB

pip install aiomysql
Cấu trúc production
FastAPI

│

├── MariaDB
│
│     Exercise
│
│     Recipe
│
│     User
│
│
├── Embedding Service
│
│     Gemini
│
│     BGE
│
│     OpenAI
│
│
├── Qdrant
│
│     Vector
│
│     Metadata
│
│
└── AI Agent
Ví dụ kết nối
from qdrant_client import AsyncQdrantClient

client = AsyncQdrantClient(
    url="http://localhost:6333"
)

Cloud

client = AsyncQdrantClient(
    url="https://xxxxx.cloud.qdrant.io",
    api_key="YOUR_API_KEY"
)
Thao tác cơ bản

Tạo collection

await client.create_collection(...)

Thêm vector

await client.upsert(...)

Tìm kiếm

await client.query_points(...)

Xóa

await client.delete(...)

Lấy thông tin

await client.get_collection(...)
Nếu dùng AI Agent (khuyến nghị)

Mình khuyên bộ stack này:

FastAPI (async)

↓

SQLAlchemy Async

↓

MariaDB (source of truth)

↓

Gemini Embedding
hoặc
BAAI/bge-m3

↓

Qdrant

↓

Gemini LLM

Đây là kiến trúc rất phổ biến cho các hệ thống RAG và AI Agent hiện đại.

Bộ thư viện đầy đủ mình khuyên
pip install \
fastapi \
uvicorn \
sqlalchemy \
aiomysql \
qdrant-client \
google-genai \
sentence-transformers

Nếu bạn hướng tới AI Agent production, thì nên học AsyncQdrantClient ngay từ đầu thay vì QdrantClient, để toàn bộ pipeline FastAPI của bạn (router → service → repository → Qdrant → LLM) đều hoạt động bất đồng bộ (async) và tận dụng tốt khả năng xử lý đồng thời.