- [RAG Introduction (Tìm tài liệu trước → rồi mới trả lời)](#rag-introduction-tìm-tài-liệu-trước--rồi-mới-trả-lời)
  - [Pipeline chuẩn (production mindset)](#pipeline-chuẩn-production-mindset)
- [Phân loại RAG](#phân-loại-rag)
  - [Retrieval (Phân loại theo cách tìm tài liệu)](#retrieval-phân-loại-theo-cách-tìm-tài-liệu)
    - [Sparse retrieval (tìm theo từ khóa)](#sparse-retrieval-tìm-theo-từ-khóa)
    - [Dense Retrieval (tìm theo “nghĩa”)](#dense-retrieval-tìm-theo-nghĩa)
    - [Hybrid Retrieval (kết hợp 2 cái)](#hybrid-retrieval-kết-hợp-2-cái)
  - [Architecture (Phân loại theo kiến trúc)](#architecture-phân-loại-theo-kiến-trúc)
    - [Naive RAG (RAG cơ bản)](#naive-rag-rag-cơ-bản)
    - [Advanced RAG](#advanced-rag)
  - [Modular RAG](#modular-rag)
  - [Agentic RAG](#agentic-rag)
- [Phân loại RAG dựa vào ứng dụng thực tế](#phân-loại-rag-dựa-vào-ứng-dụng-thực-tế)
  - [Knowledge RAG (RAG truyền thống)](#knowledge-rag-rag-truyền-thống)
  - [Tool RAG (Retrival Tool)](#tool-rag-retrival-tool)
  - [SQL RAG (Không retrieve tài liệu. Retrieve schema)](#sql-rag-không-retrieve-tài-liệu-retrieve-schema)
  - [API RAG (Retrieve API](#api-rag-retrieve-api)
  - [Hybrid RAG (Đây là loại phổ biến nhất trong doanh nghiệp)](#hybrid-rag-đây-là-loại-phổ-biến-nhất-trong-doanh-nghiệp)
  - [Graph RAG (Không lưu vector. Mà lưu Graph)](#graph-rag-không-lưu-vector-mà-lưu-graph)
  - [Agentic RAG (Đây là xu hướng hiện nay)](#agentic-rag-đây-là-xu-hướng-hiện-nay)
  - [Multi-Modal RAG (Không chỉ text. Có thể retrieve Image, Video, ...)](#multi-modal-rag-không-chỉ-text-có-thể-retrieve-image-video-)
---
# RAG Introduction (Tìm tài liệu trước → rồi mới trả lời)
```bash
Vấn đề của AI thông thường: 
    - Các mô hình như ChatGPT chỉ biết những gì đã được huấn luyện trước đó.
    - Ví dụ: Em hỏi: “Quy định nội bộ công ty ABC về nghỉ phép là gì?” AI không biết, vì tài liệu đó không có trong dữ liệu huấn luyện. => Đây là lúc RAG xuất hiện.

Thay vì:
    - AI trả lời dựa hoàn toàn vào trí nhớ
    - Thì RAG: AI đi tìm tài liệu liên quan, đọc nó, rồi trả lời dựa trên tài liệu đó
```
**Trong RAG có phải luôn phải nạp tài liệu không?**
```bash
Không. Có hai kiểu phổ biến:
    Kiểu 1: RAG trên tài liệu riêng
        Ví dụ: chatbot nội bộ công ty.
            Bạn nạp: employee_handbook.pdfcompany_policy.pdf
            
            Pipeline: PDF -> Chunking -> Embedding -> Vector Database -> Retrieval -> LLM

            Người dùng hỏi:
                Công ty có bao nhiêu ngày nghỉ phép?

            Retriever tìm đúng đoạn trong handbook rồi đưa cho LLM.

    Kiểu 2: Web RAG
        Không có tài liệu cố định.
        
        Pipeline: User Query -> Search Engine -> Web Pages -> Retriever -> LLM
        
        Ví dụ:
            Giá vàng hôm nay
        Hệ thống:
            - Search Google/Bing
            - Lấy vài trang mới nhất
            - Trích nội dung
            - Đưa cho LLM trả lời
```
**ChatGPT, Gemini, Claude có dùng RAG để tìm web không?**
```bash
Có, khi bật khả năng tìm kiếm.

Ví dụ bạn hỏi: Thời tiết Hà Nội hôm nay
    LLM không thể biết chính xác vì dữ liệu huấn luyện đã cũ.
    
    Khi hỏi "Thời tiết Hà Nội hôm nay" thì chuyện gì xảy ra?
        Thông thường:
            1. User:"Thời tiết Hà Nội hôm nay?"       
            2. LLM Router       
            3. Phát hiện cần dữ liệu realtime       
            4. Search API / Weather API       
            5. Kết quả: - 31°C - Mưa rào - Độ ẩm 80%       
            6. LLM sinh câu trả lời tự nhiên
        => Thực tế nhiều hệ thống không đi tìm trên web tự do mà gọi thẳng API thời tiết vì dữ liệu chính xác và có cấu trúc hơn.
        => Đây chính là RAG kết hợp web search.
```
**Nếu không dùng RAG thì sao?**
```bash
LLM chỉ dựa vào trọng số đã học.

Ví dụ hỏi:
    Thủ đô Việt Nam là gì?
=> Không cần RAG. Vì kiến thức này đã nằm trong tham số của mô hình.
Người ta gọi là: Parametric Memory (kiến thức nằm trong weights).

Ngược lại:
    Giá Bitcoin hiện tại là bao nhiêu?

    Thông tin thay đổi từng giây. Không thể lưu trong weights.
    Phải dùng: External Memory → RAG/Search.
```
**Nhóm công cụ phổ biến**
```bash
1. Bộ công cụ phổ biến nhất hiện nay
    - LangChain: Đây là framework RAG nổi tiếng nhất. Nó cung cấp gần như mọi thứ:
        + Load PDF
        + Chunking
        + Embedding
        + Vector Database
        + Retrieval
        + Prompt
        + LLM

        Ưu điểm:
            - Hệ sinh thái lớn
            - Nhiều ví dụ
            - Hỗ trợ hầu hết model
        Nhược điểm:
            - Khá nặng
            - API thay đổi thường xuyên
            - Nhiều abstraction khiến khó hiểu bản chất

    - LlamaIndex: Framework sinh ra gần như chỉ để làm RAG.
        Ưu điểm:
            - Tập trung vào retrieval
            - Dễ làm chatbot hỏi đáp tài liệu
            - Tích hợp nhiều vector database
        Nhược điểm:
            - Ít linh hoạt hơn LangChain
            - Nếu mới học RAG: LlamaIndex thường dễ tiếp cận hơn.

2. Embedding Model: RAG luôn cần embedding model.
    - BAAI/bge-small-en
    - BAAI/bge-large-en # Chất lượng cao hơn.
    - multilingual-e5-large # Rất tốt cho tiếng Việt.
    - intfloat/multilingual-e5-large
    - OpenAI Embedding
    - text-embedding-3-small # Nếu chấp nhận trả phí.

3. Vector Database: Nơi lưu embedding.
    - FAISS # Thường dùng nhất khi học. Facebook phát triển.
        Ưu điểm:
            - Nhanh
            - Chạy local
            - Không cần server
    - ChromaDB: Rất phổ biến trong các project nhỏ.
        Ưu điểm:
            - Dễ dùng hơn FAISS
            - Có metadata
    - Qdrant: Khi triển khai thực tế. Phù hợp hệ thống lớn.
        Ưu điểm:
            - Hiệu năng cao
            - API đẹp
            - Hỗ trợ hybrid search
            - Milvus
```
**Stack mà nhiều người đang dùng hiện nay**
```bash
1. Học RAG từ gốc
    sentence-transformers+FAISS+OpenAI/Llama
    Bạn sẽ hiểu:
        - Chunking
        - Embedding
        - Similarity Search
        - Retrieval

2. Làm dự án nhỏ
    LlamaIndex+ChromaDB+OpenAI # Code rất ít.

3. Production
    LangChain hoặc LlamaIndex+Qdrant+OpenAI / Claude / Gemini / Llama
```
**Pipeline**
```bash
User hỏi → tìm tài liệu → nhét vào prompt → LLM trả lời
```
**3 khối trong RAG**
```bash
1. Retriever (trái tim của RAG)
    - Nhiệm vụ: Tìm tài liệu liên quan nhất
    - Có 3 loại (từ paper):
        1. Sparse retrieval:
            - BM25 (kiểu Google search)
            - dựa vào keyword
            - mạnh: chính xác literal
            - yếu: không hiểu nghĩa
        2. Dense retrieval (vector)
            - embedding + cosine similarity
            - mạnh: hiểu semantic
            - yếu: đôi khi “đoán sai”
        3. Hybrid (pro dùng cái này)
            - kết hợp BM25 + vector => đây là best practice trong industry  
2. Chunking (cái mà paper ít nói nhưng cực quan trọng)
    - Bạn KHÔNG đưa cả document vào. bạn phải chia nhỏ (chunk)
    - Quy tắc: 200–500 tokens, có overlap (10–20%)
    - Vì:
        + nhỏ quá → mất context
        + to quá → search kém
    => Đây là thứ quyết định 80% chất lượng RAG 
3. Embedding
    - Chuyển text → vector
    - Lưu ý quan trọng:
        + embedding model ≠ LLM
        + embedding quyết định retrieval quality (chất lượng truy xuất)
4. Generator (LLM)
    - chỉ làm 1 việc: viết lại câu trả lời dựa trên context
    - Nếu RAG sai: 80% lỗi ở retriever, KHÔNG phải LLM
```
## Pipeline chuẩn (production mindset)
```bash
Pipeline chuẩn từ paper → thực tế:
- Offline:
    1. Load document
    2. Chunk
    3. Embed
    4. Lưu vào vector DB
- Online:
    1. User hỏi
    2. Embed query
    3. Retrieve top-k chunks
    4. Inject vào prompt
    5. LLM trả lời
```
# Phân loại RAG
```bash
Cách 1: Phân loại theo retrieval (cách tìm tài liệu - truy xuất tài liệu)
    1. Sparse retrieval
    2. Dense retrieval
    3. Hybrid retrieval
Cách 2: Phân loại theo kiến trúc RAG (pipeline)
    1. Naive RAG
    2. Advanced RAG
    3. Modular / Agentic RAG
```
## Retrieval (Phân loại theo cách tìm tài liệu)
### Sparse retrieval (tìm theo từ khóa)
**Ex**
```bash
Tưởng tượng bạn đang tìm tài liệu. Bạn có 1 “database” gồm các câu:
    1. "Hà Nội hôm nay trời mưa"
    2. "Thời tiết ở Hà Nội rất đẹp"
    3. "Tôi thích ăn phở bò"

❓ Bạn hỏi: “Hà Nội hôm nay thời tiết thế nào?” thì Sparse Retrieval (tìm theo từ khóa)

👉 Cách nó hoạt động:
    - nhìn vào từng từ trong câu hỏi
    - so với từng từ trong document
    - Ví dụ: Hà Nội hôm nay thời tiết
        + So sánh:
            1	Hà Nội, hôm nay
            2	Hà Nội, thời tiết
            3	❌ không match
    👉 kết quả: câu 1 và 2 đều được chọn

🧠 Bản chất: so khớp keyword (exact match)

👍 Ưu điểm:
    - chính xác khi từ giống nhau
    - dễ hiểu
👎 Nhược điểm:
    - không hiểu nghĩa
```
**Ex2: Ví dụ fail:**
```bash
Query: “thời tiết thủ đô” 👉 nhưng document viết: “Hà Nội”
→ ❌ không match
```
### Dense Retrieval (tìm theo “nghĩa”)
```bash
Cách nó hoạt động: biến câu thành vector (embedding) và so sánh ý nghĩa.
    Dense Retrieval hiểu ngữ nghĩa nhờ mô hình Deep Learning (Transformer/Embedding Model).
```
**Dense Retrieval có phải là LLM không?**
```bash
Không hẳn. Thường có hai mô hình riêng:

- Retriever: Biến câu hỏi và tài liệu thành vector.
    Ví dụ:
        - DPR
        - Contriever
        - BGE
        - E5
        - GTE

- Generator: Sinh câu trả lời.
    Ví dụ:
        - GPT
        - Claude
        - Gemini
        - Llama
```
**Pipeline đầy đủ**
```bash
Question -> Retriever(Dense Retrieval) -> Top-k Documents -> Generator (LLM) -> Answer
=> Đây chính là kiến trúc RAG cổ điển.
```
**Tại sao Dense Retrieval lại hiểu được ngũ nghĩa**
```bash
1. Bên trong nó có mô hình Deep Learning.
    Cách tìm kiếm truyền thống (Sparse Retrieval)
        - Ví dụ tài liệu: "Hà Nội hôm nay trời mưa lớn"
        - Người dùng hỏi: "Thời tiết thủ đô Việt Nam hiện tại thế nào?"

        Tìm kiếm kiểu keyword như BM25 sẽ gặp khó khăn vì:
            - Không có từ "thời tiết"
            - Không có từ "thủ đô Việt Nam"
            - Chỉ có "Hà Nội"
        => Keyword không khớp nhiều.

    Dense Retrieval dùng một neural network (thường là Transformer) để biến văn bản thành vector.
        Ví dụ:
            "Tình hình thời tiết Hà Nội hôm nay"
                    ↓
            [0.12, -0.45, 0.89, ...]

            "Thời tiết thủ đô Việt Nam hiện tại"
                    ↓
            [0.10, -0.43, 0.91, ...]

        Mặc dù câu khác nhau hoàn toàn nhưng vector lại gần nhau trong không gian embedding.

        Hệ thống sẽ tính:
            - Cosine Similarity
            - Dot Product
        => để tìm vector gần nhất.

        Ý tưởng là:
            Những câu có ý nghĩa giống nhau sẽ nằm gần nhau trong không gian vector.

2. Mô hình Deep Learning đó được huấn luyện thế nào?
    Ví dụ:
        - Query: "Xe điện tốt nhất hiện nay"
        - Document: "Tesla Model Y là mẫu xe điện bán chạy nhất" => Đây là cặp đúng.

        Cặp sai:
            - Query: "Xe điện tốt nhất hiện nay"
            - Document: "Cách nấu phở bò"
        => Cặp sai.

    Trong quá trình training:
        Mô hình học để:
            - Similarity(query, positive_doc) ↑
            - Similarity(query, negative_doc) ↓

    Sau hàng triệu cặp dữ liệu:
        Nó học được:
            - car ≈ automobile
            - doctor ≈ physician
            - Hà Nội ≈ thủ đô Việt Nam
        mà không cần trùng từ khóa.
```
**Ex1**
```bash
Query: “thời tiết thủ đô”
Model hiểu: “thủ đô” ≈ “Hà Nội”
👉 nó sẽ chọn: "Hà Nội hôm nay trời mưa"
🧠 Bản chất:
    - so sánh semantic (ngữ nghĩa)
    👍 Ưu điểm:
        + hiểu nghĩa
        + không cần trùng từ
    👎 Nhược điểm:
        + đôi khi “đoán sai”
        + có thể chọn câu không liên quan
```
**Ex2: Ví dụ fail:**
```bash
Query: “tôi thích ăn” 👉 nó có thể chọn: “tôi thích đi du lịch” 😄 
→ vì “semantic gần”
```
### Hybrid Retrieval (kết hợp 2 cái)
```bash
👉 dùng cả:
    + sparse (keyword)
    + dense (semantic)
```
**Ex**
```bash
Query: “thời tiết Hà Nội”
👉 hệ thống sẽ:
    + check keyword: “Hà Nội”
    + check meaning: “thời tiết”
👉 kết quả chính xác hơn
```
## Architecture (Phân loại theo kiến trúc)
### Naive RAG (RAG cơ bản)
```bash
Đây là phiên bản đơn giản nhất
```
**Pipeline**
```bash
Tài liệu
    ↓
Chunking
    ↓
Embedding
    ↓
Vector DB

====================

Câu hỏi
    ↓
Embedding
    ↓
Vector Search
    ↓
Top-k Chunks
    ↓
LLM
    ↓
Trả lời
```
**Ex**
```bash
Tài liệu:
    Công ty cho nhân viên nghỉ phép 12 ngày/năm.

Người dùng hỏi:
    Tôi được nghỉ phép bao nhiêu ngày?

Retriever tìm thấy chunk đó rồi gửi cho LLM:
    Context: "Công ty cho nhân viên nghỉ phép 12 ngày/năm"

Question:
    "Tôi được nghỉ phép bao nhiêu ngày?"

LLM trả lời:
    12 ngày mỗi năm.
```
**Vấn đề của Naive RAG**
```bash
Giả sử tài liệu có:
    - Nhân viên chính thức: 12 ngày phép
    - Nhân viên thử việc: 0 ngày phép

Người dùng hỏi:
    Nhân viên thử việc được nghỉ bao nhiêu ngày?

Retriever có thể lấy nhầm chunk:
    Nhân viên chính thức: 12 ngày phép → Trả lời sai.

Tức là:
    Naive RAG chỉ làm:
        Search
         ↓
        LLM
    Không có bước kiểm tra gì thêm.
```
### Advanced RAG
```bash
Người ta nhận ra:
    Không phải chunk nào tìm được cũng tốt.
Nên thêm nhiều bước cải tiến.
```
**Pipeline**
```bash
Question
    ↓
Query Rewrite
    ↓
Retrieval
    ↓
Reranking
    ↓
Top Chunks
    ↓
LLM
```
**Kỹ thuật 1: Query Rewriting**
```bash
Người dùng hỏi:
    Tôi được nghỉ phép bao nhiêu ngày?

Nhưng tài liệu ghi:
    Annual Leave Policy

Retriever khó tìm.
Hệ thống tự đổi câu hỏi thành:
    Annual leave policy for employees

rồi mới search.
```
**Kỹ thuật 2: Reranking**
```bash
Giả sử Retriever lấy được:
    - Chunk A: nhân viên chính thức
    - Chunk B: nhân viên thử việc
    - Chunk C: bảo hiểm
Retriever chỉ dựa vào embedding.

Sau đó có một model khác:
    - Cross Encoder
    - đọc: Question + Chunk
và chấm điểm lại.

Ví dụ:
    - Chunk A = 0.70
    - Chunk B = 0.95
    - Chunk C = 0.10
Kết quả:
    - Chunk B
    - Chunk A
    - Chunk C
được sắp xếp lại.

Đây là lý do Advanced RAG thường chính xác hơn rất nhiều.
```
**Kỹ thuật 3: Hybrid Search**
```bash
Không chỉ tìm bằng embedding.

Kết hợp:
    Dense Search
    +
    Keyword Search

Ví dụ:
    Mã lỗi ERR-1001

    - Embedding thường xử lý kém các mã lỗi.
    - Keyword Search lại rất mạnh.
=> Nên kết hợp cả hai.
```
## Modular RAG
```bash
Lúc này người ta không còn dùng một pipeline cố định nữa. Thay vào đó:
    Question
       ↓
    Decision
       ↓
    Tool nào phù hợp?
```
**Ex**
```bash
Người dùng hỏi:
    Tài liệu nhân sự nói gì về nghỉ phép?
→ Search HR docs

Người dùng hỏi:
    Giá Bitcoin hôm nay?
→ Search Web

Người dùng hỏi:
    Doanh thu tháng trước?
→ Query Database

Hệ thống có nhiều nguồn dữ liệu:
    - PDF
    - SQL
    - API
    - Website
    - Vector DB
    - và tự chọn.
```
**Pipeline**
```bash
      Question
           ↓
      Router
    ↙   ↓   ↘
SQL  Web  VectorDB
    ↘   ↓   ↙
       LLM
```
## Agentic RAG
```bash
Đây là phiên bản "chủ động suy nghĩ". Không chỉ search một lần. Nó có thể:
    Search
     ↓
    Đánh giá kết quả
     ↓
    Search lại
     ↓
    Tìm nguồn khác
     ↓
    Tổng hợp
```
**Ex**
```bash
Người dùng hỏi:
    So sánh doanh thu 2024 với 2025

Agent có thể tự lập kế hoạch:
    Bước 1: Lấy doanh thu 2024
    Bước 2: Lấy doanh thu 2025
    Bước 3: Tính phần trăm tăng trưởng
    Bước 4: Viết báo cáo

Nó giống:
    - Nhân viên phân tích dữ liệu hơn là Máy tìm kiếm
```
# Phân loại RAG dựa vào ứng dụng thực tế
```bash
Nếu nói theo nghiên cứu và sản phẩm hiện nay thì không có một tiêu chuẩn chính thức kiểu "RAG có đúng 5 loại". 
    Nhưng trong thực tế, người ta thường chia thành khoảng 7–8 kiến trúc RAG phổ biến. Chúng khác nhau ở chỗ retrieve cái gì và retrieve như thế nào
```
## Knowledge RAG (RAG truyền thống)
```bash
Đây là thứ mọi người nghĩ đến nhiều nhất

Đây là kiến trúc của:
    - ChatPDF
    - AskYourPDF
    - NotebookLM
    - Chat với tài liệu
=> Đây là RAG cơ bản nhất.
```
**Architecture (kiến trúc)**
```bash
PDF
Word
Excel
Website
Wiki
...
↓
Chunk
↓
Embedding
↓
Vector DB
↓
Top K
↓
LLM
↓
Answer
```
**Ex**
```bash
Hỏi:
    Chính sách hoàn tiền là gì?
    ↓
    Tìm trong PDF
    ↓
    Lấy đoạn liên quan
    ↓
    LLM trả lời
```
## Tool RAG (Retrival Tool)
```bash
Framework Agent hiện nay dùng rất nhiều.
    Ví dụ:
        - LangGraph
        - LlamaIndex Agent
        - CrewAI
        - OpenAI Agent SDK
```
**Ex**
```bash
Tool Description
↓
Embedding
↓
Vector DB
↓
User
↓
Embedding
↓
Top K Tool
↓
LLM
↓
Function Calling
```
**Ex**
```bash
Đổi địa chỉ
↓
retrieve
↓
update_address
↓
call tool
```
## SQL RAG (Không retrieve tài liệu. Retrieve schema)
**Ex**
```bash
Database
    - users
    - orders
    - products
    - payments

Embedding
users
description...
orders
description...

User
    Doanh thu tháng này?
↓
retrieve
    - orders
    - payments
↓
LLM sinh SQL
    SELECT ...
=> Đây cũng là RAG.
```
## API RAG (Retrieve API
**Ex**
```bash
- Weather API
- Google Calendar API
- Email API
- Maps API
- ...

Embedding description.
    User: Mai Hà Nội có mưa không?
    ↓
    retrieve: Weather API
    ↓
    LLM gọi API.
```
## Hybrid RAG (Đây là loại phổ biến nhất trong doanh nghiệp)
```bash
Không chỉ Vector Search.
    Mà là
        User
        ↓
        BM25 + Embedding
        ↓
        Fusion
        ↓
        Top K
```
**Ex**
```bash
"GPT-4.1"
    - Embedding đôi khi tìm không tốt.
    - BM25 lại rất mạnh với keyword.
    => Người ta kết hợp cả hai: BM25 + Vector = Hybrid Search
        - Milvus
        - Weaviate
        - Elastic
        - Azure AI Search
        => đều hỗ trợ.
```
## Graph RAG (Không lưu vector. Mà lưu Graph)
**Ex**
```bash
Steve Jobs
↓
Founder
↓
Apple
↓
Developed
↓
iPhone

User: Ai tạo ra iPhone?
    LLM truy vấn Graph.
        Steve Jobs
        ↓
        Apple
        ↓
        iPhone
=> Microsoft đang đầu tư khá mạnh vào GraphRAG. Nó tốt khi dữ liệu có nhiều quan hệ.
```
## Agentic RAG (Đây là xu hướng hiện nay)
```bash
Không retrieve một lần. Mà Agent tự quyết định.
    User
    ↓
    Search
    ↓
    Không đủ
    ↓
    Search tiếp
    ↓
    Không đủ
    ↓
    Search Web
    ↓
    Đọc PDF
    ↓
    Gọi Tool
    ↓
    Answer
=> Có nhiều vòng retrieve.
```
**Ex**
```bash
User
↓
Search PDF
↓
Không thấy
↓
Search Internet
↓
Không thấy
↓
Search SQL
↓
Không thấy
↓
Hỏi tiếp user
↓
Answer
=> Thằng Agent sẽ tự lập kế hoạch.
```
## Multi-Modal RAG (Không chỉ text. Có thể retrieve Image, Video, ...)
**Ex**
```bash
Ảnh hóa đơn
↓
Embedding
↓
Retrieve
↓
LLM

Hoặc

Ảnh X-ray
↓
Retrieve case tương tự
↓
LLM
=> Đây là hướng đang phát triển rất mạnh.
```