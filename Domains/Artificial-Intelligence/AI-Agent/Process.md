- [Embedding (chuyển dữ liệu thành vector số)](#embedding-chuyển-dữ-liệu-thành-vector-số)
- [Similarity Search](#similarity-search)
- [Qdrant (để lưu vector)](#qdrant-để-lưu-vector)
- [Hybrid Search](#hybrid-search)
- [Redis (một cuốn sổ ghi chú siêu nhanh)](#redis-một-cuốn-sổ-ghi-chú-siêu-nhanh)
- [LangSmith (để quan sát, debug, đánh giá và kiểm thử ứng dụng LLM/AI Agent)](#langsmith-để-quan-sát-debug-đánh-giá-và-kiểm-thử-ứng-dụng-llmai-agent)
- [Ask (câu hỏi liên quan đến AI agent)](#ask-câu-hỏi-liên-quan-đến-ai-agent)
  - [Có fine-tune được AI Agent không?](#có-fine-tune-được-ai-agent-không)
  - [nếu hỏi AI mà AI trả lời sai thì em sẽ xử lý thế nào, kiểu mình cần lấy thông tin A mà nó nói thông tin B](#nếu-hỏi-ai-mà-ai-trả-lời-sai-thì-em-sẽ-xử-lý-thế-nào-kiểu-mình-cần-lấy-thông-tin-a-mà-nó-nói-thông-tin-b)
  - [khi cho AI gọi API tức là đang cho AI đọc thẳng dữ liệu vào db thì có sợ bị lộ thông tin không, em sẽ xử lý bằng cách nào](#khi-cho-ai-gọi-api-tức-là-đang-cho-ai-đọc-thẳng-dữ-liệu-vào-db-thì-có-sợ-bị-lộ-thông-tin-không-em-sẽ-xử-lý-bằng-cách-nào)
- [Ask (Câu hỏi liên quan đến tích hợp AI Agent)](#ask-câu-hỏi-liên-quan-đến-tích-hợp-ai-agent)
- [Vector Index](#vector-index)
---
# Embedding (chuyển dữ liệu thành vector số)
**Ex**
```bash
Bench Press
    ↓
Embedding Model
    ↓
[0.12, 0.44, 0.55, ...]
```
# Similarity Search
```bash
Thay vì
    WHERE name='Bench Press'

ta hỏi
    Vector nào gần nhất?

Có 3 cách đo.
    - Euclidean Distance (Khoảng cách)
    - Dot Product
    - Cosine Similarity (Đây là cái dùng nhiều nhất)
```
# Qdrant (để lưu vector)
```bash
Qdrant/pgvector chỉ chịu trách nhiệm tìm kiếm ngữ nghĩa cực nhanh.
LLM chỉ nhận những tài liệu liên quan nhất thay vì toàn bộ cơ sở dữ liệu.

Ưu điểm
    - Rất nhanh
    - RAM tối ưu
    - HNSW
    - Filtering
    - Payload
    - Distributed

Nhược điểm
    - Không JOIN
    - Không Transaction như PostgreSQL
```
**Ex**
```bash
Point 
    - id=1
    - vector=[...]
    - payload
        {
            "name":"Bench Press",
            "muscle":"Chest"
        }

Query
    Query Vector
        ↓
    Qdrant
        ↓
    Top 10 nearest
=> Không cần SQL.
```
# Hybrid Search
```bash
Production gần như không chỉ dùng Vector Search.
```
**Ex**
```bash
Người dùng hỏi: Chest exercise

Pipeline
    User
    ↓
    Embedding
    ↓
    Vector Search
    ↓
    Top 100
    ↓
    SQL Filter
    ↓
    Business Logic
    ↓
    LLM

Hoặc
    User
    ↓
    Keyword Search (BM25) + Vector Search
    ↓
    Merge Ranking
    ↓
    Top K
    ↓
    LLM

=> Đây gọi là Hybrid Search, giúp vừa bắt được từ khóa chính xác vừa hiểu ngữ nghĩa.
```
**AI Agent Pipeline Production**
```bash
Đây là kiến trúc mà hầu hết các hệ thống AI hiện đại sử dụng.

    User Question
          │
          ▼
    Embedding Model
          │
          ▼
    Vector Database (Qdrant / pgvector)
          │
          ▼
    Top-K Similar Documents
          │
          ▼
    Metadata Filter
    (muscle=Chest, difficulty=Beginner...)
          │
          ▼
    Business Logic
          │
          ▼
    LLM (Gemini/OpenAI)
          │
          ▼
    Final Response
```
# Redis (một cuốn sổ ghi chú siêu nhanh)
```bash
Nó không phải database chính như MariaDB.

Đặc điểm:
    - Đọc: khoảng vài trăm micro giây đến vài mili giây.
    - Ghi: rất nhanh.
    - Có thể tự xóa dữ liệu sau một thời gian (TTL).
    - Không dùng để lưu dữ liệu quan trọng lâu dài.

So sánh
    MariaDB
        User
        ↓
        SELECT
        ↓
        Đọc từ ổ cứng

    Redis
        User
        ↓
        GET
        ↓
        Đọc trực tiếp từ RAM
    => RAM nhanh hơn SSD rất nhiều.
```
**Trong AI Agent, thường có 4 mục đích lớn**
```bash
1. Session
    Ví dụ:
        User đăng nhập. -> Sau khi login thành công.
            Server tạo
                session_id: abc123xyz
                Redis lưu
                Key session:abc123xyz
                ↓
                Value
                    { 
                        user_id:15,
                        role:"premium",
                        expire:30 phút
                    }
            
            Lần request tiếp theo.
                Browser gửi
                    Cookie
                    abc123xyz

                Server
                ↓
                Redis
                ↓
                Lấy được: user_id=15 (Không cần query MariaDB) -> Nhanh hơn.

    Session Pipeline
        Login
        ↓
        MariaDB
        ↓
        Password đúng
        ↓
        Redis (session:abc123)
        ↓
        Browser lưu Cookie
        ↓
        Request mới
        ↓
        Redis
        ↓
        User

2. Cache
    Ví dụ: Có API GET /exercises
        Trong DB: 10000 bài tập
        Mỗi request: SELECT * FROM exercise -> Tốn.
        Thay vào đó. Lần đầu:
            Client
            ↓
            MariaDB
            ↓
            10000 exercise
            ↓
            Redis Cache
        Lần sau
            Client
            ↓
            Redis
            ↓
            Trả luôn: Không cần query SQL.

3. Conversation State
    Đây là phần AI Agent dùng rất nhiều.

    Ví dụ.
        Bạn chat
            User: Tôi muốn giảm cân.
            AI  : Được.
        Sau đó
            User: Nam. 25 tuổi. 70kg. Rồi. Tôi nên ăn gì? Nếu AI không nhớ. Nó sẽ hỏi lại.
            Redis sẽ lưu. conversation:abc
                {
                    goal:"lose weight",
                    gender:"male",
                    age:25,
                    weight:70
                }
        Lần prompt sau.
            AI đọc.
            ↓
            Biết ngay.

    Pipeline
        Prompt
        ↓
        Redis
        ↓
        Conversation State
        ↓
        LLM
        ↓
        Update State
        ↓
        Redis

4. Pending Actions
    Đây là phần rất nhiều AI Agent production sử dụng.

    Ví dụ.
        User: Đặt lịch tập cho ngày mai.
        AI  : Bạn có chắc không?
        User: Chưa trả lời.
            Redis lưu: pending_action {
                type:"create_workout",
                date:"tomorrow"
            }

        5 phút sau.
            User: Đồng ý.
            AI
            ↓
            Redis
            ↓
            Ồ. Đang chờ action
            ↓
            Thực hiện luôn.

        Nếu không có Redis. AI sẽ quên.

    Pipeline
        User
        ↓
        AI
        ↓
        Pending Action
        ↓
        Redis
        ↓
        Sau User: OK
        ↓
        Redis
        ↓
        Action
        ↓
        Database
```
# LangSmith (để quan sát, debug, đánh giá và kiểm thử ứng dụng LLM/AI Agent)
```bash
LangSmith không phải là framework. Nó là một nền tảng (platform)
    Nó giống như:
        Với Backend → có Grafana, Prometheus, Jaeger
        Với AI Agent → có LangSmith

So sánh:
    - LangChain: Framework viết AI Agent
    - LangGraph: Framework xây AI Workflow/Agent phức tạp
    - LangSmith: Monitoring + Debug + Evaluation
```
**LangSmith làm gì?**
```bash
Giả sử AI Agent của bạn.
    User
    ↓
    Gemini
    ↓
    Tool Calling
    ↓
    MariaDB
    ↓
    Gemini
    ↓
    Response

Một ngày AI trả lời sai.
    Bạn sẽ hỏi: Sai ở đâu?
    
    Nếu không có LangSmith.
        Bạn chỉ có print(prompt) hoặc logger.info(...) -> Khá cực.

Có LangSmith.
    Bạn mở dashboard. -> Thấy toàn bộ.
        Request
        ↓
        System Prompt
        ↓
        User Prompt
        ↓
        LLM Response
        ↓
        Tool Calling
        ↓
        SQL
        ↓
        Output
        ↓
        Final Answer
=> Toàn bộ pipeline hiện ra.
```
**Workflow**
```bash
User: Lập lịch tập cho tôi.

LangSmith hiển thị
    Trace Request
↓
Prompt
↓
Gemini
↓
Tool: get_user_profile()
↓
Tool: search_exercise()
↓
Gemini
↓
Final Response
=> Bạn click từng bước. Biết ngay nó lưu gì?
```
# Ask (câu hỏi liên quan đến AI agent)
## Có fine-tune được AI Agent không?
```bash
Về mặt bản chất kỹ thuật, việc sử dụng LangChain hay LangGraph để xây dựng AI Agent, cấu hình RAG hay thiết lập quy trình duyệt đồ thị cho Chatbot thì không gọi là Fine-tune. Đó là quá trình Prompt Engineering, In-Context Learning và Agentic Workflow Architecture
    tức là chúng ta tối ưu hóa luồng xử lý và ngữ cảnh đầu vào cho LLM mà không hề can thiệp hay thay đổi trọng số (weights) của mô hình gốc.

Còn nếu muốn Fine-tune LLM thực sự, em sẽ có 2 hướng tiếp cận:
    - Với Closed-source (như GPT, Gemini): Em sẽ chuẩn bị dataset dạng JSONL, dùng API Fine-tuning của hãng để upload dữ liệu lên server của họ, nhờ hạ tầng của họ cập nhật trọng số và tạo ra một custom endpoint riêng.

    - Với Open-source (như Llama 3, Qwen): Em sẽ tự thuê GPU, áp dụng các kỹ thuật PEFT (Parameter-Efficient Fine-Tuning) như LoRA hoặc QLoRA để đóng băng mạng gốc, chỉ train một vài nhánh bổ trợ nhằm tiết kiệm VRAM và tối ưu hóa mô hình theo dữ liệu riêng."
```
## nếu hỏi AI mà AI trả lời sai thì em sẽ xử lý thế nào, kiểu mình cần lấy thông tin A mà nó nói thông tin B
```bash
Chia làm 3 tầng phòng thủ cụ thể: 
    - Tầng Dữ liệu
    - Tầng Kiểm soát (Guardrails) 
    - Tầng Trải nghiệm người dùng.

Bạn có thể trả lời trực diện hội đồng phỏng vấn theo cấu trúc mạch lạc dưới đây:
    Bước 1: Khắc phục gốc rễ bằng kiến trúc RAG và Tooling (Tầng Dữ liệu)
        Hiện tượng AI trả lời sai (Hallucination) thường do nó thiếu ngữ cảnh thực tế hoặc bị "bịa" dựa trên trọng số cũ.

        Em sẽ không để AI tự suy diễn. Thay vào đó, em áp dụng kiến trúc RAG (Retrieval-Augmented Generation) để ép AI chỉ được đọc thông tin từ một nguồn đáng tin cậy (Cơ sở dữ liệu, tài liệu hệ thống).

        Nếu AI cần gọi API để lấy thông tin A, em sẽ sử dụng cơ chế Function Calling (như with_structured_output hoặc LangGraph Tools). Em ràng buộc đầu ra của API bằng Pydantic Schema để ép AI phải trả về đúng cấu trúc JSON định sẵn (ví dụ: bắt buộc phải có trường info_A). Nếu API trả về thiếu hoặc sai định dạng, hệ thống sẽ tự động bắt lỗi (Validation Error) trước khi đưa đến người dùng.

    Bước 2: Thiết lập màng lọc tự động đánh giá (Tầng Guardrails)
        Em sẽ dựng một lớp trung gian để kiểm định câu trả lời của AI trước khi in ra màn hình cho user.

        Sử dụng các thư viện Guardrails (hoặc dùng một LLM nhỏ hơn, rẻ hơn) làm nhiệm vụ phân loại độc lập. Lớp này sẽ chạy một prompt kiểm tra nhanh: "Câu trả lời B có chứa thông tin A mà người dùng yêu cầu hay không?".

        Nếu kết quả kiểm tra là Không, hệ thống sẽ chặn câu trả lời đó lại ngay lập tức, không cho hiển thị ra Frontend để tránh làm nhiễu thông tin của người dùng.

    Bước 3: Định tuyến lại luồng xử lý (Fallback Strategy & UX)
        Khi hệ thống phát hiện AI đã trả lời sai hoặc không tìm thấy thông tin A sau một số lần thử lại (Retry) không thành công, em sẽ kích hoạt kịch bản dự phòng (Fallback):

        Về mặt hệ thống: Trả về một câu trả lời an toàn đã được định nghĩa cứng (Hard-coded) bởi lập trình viên, ví dụ: "Hệ thống hiện chưa tìm thấy thông tin chính xác về [A]. Vui lòng thử lại hoặc liên hệ hỗ trợ." thay vì để AI tiếp tục nói nhảm.

        Về mặt vận hành: Ghi nhận (Log) lại toàn bộ trường hợp lỗi này vào hệ thống giám sát (như LangSmith hoặc các file log) để đội ngũ kỹ sư có thể đánh giá, tinh chỉnh lại dữ liệu hoặc prompt cho các phiên bản sau."
```
## khi cho AI gọi API tức là đang cho AI đọc thẳng dữ liệu vào db thì có sợ bị lộ thông tin không, em sẽ xử lý bằng cách nào
```bash
Xử lý bằng 3 lớp phòng thủ sau:
    1. Tuyệt đối không cho AI kết nối trực tiếp vào DB (Database Level)
        AI Agent không bao giờ được cầm tài khoản Root hay có quyền chạy các câu lệnh SQL thuần (SELECT * FROM...). AI chỉ được phép tương tác thông qua một lớp trung gian (Abstraction Layer) là các hàm API được định nghĩa sẵn.

        Cách xử lý: Bạn dùng cơ chế Function Calling (ví dụ: with_structured_output() hoặc LangGraph Tools). Bạn chỉ cung cấp cho AI các "công cụ" (Tools) có phạm vi rất hẹp, ví dụ: Hàm get_user_profile(user_id) chỉ lấy đúng thông tin cá nhân của ID đó, chứ không cho nó hàm generic kiểu execute_query(sql_string).

    2. Ép AI tuân thủ phân quyền (Application Level)
        Đây là nơi bạn tận dụng AuthContext từ Frontend kết hợp với Backend (FastAPI/SQLAlchemy) của bạn:

        Cách xử lý: Khi người dùng gửi một yêu cầu qua Chatbot, Backend phải bắt được user_id hoặc token từ AuthContext của người dùng đó. Khi AI quyết định gọi một API để lấy dữ liệu, bạn phải ép API đó kiểm tra quyền sở hữu.

    3. Bộ lọc dữ liệu đầu ra (Data Masking & PII Filter)
        Đôi khi AI gọi đúng API, lấy đúng dữ liệu của chính user đó, nhưng trong đống dữ liệu trả về từ DB lại chứa các thông tin cực kỳ nhạy cảm như Mật khẩu đã mã hóa (Hashed Password), Token, Mã số định danh, Số thẻ tín dụng... và AI vô tình in thẳng đống này lên màn hình chat.

        Cách xử lý:
            Tại tầng API/SQLAlchemy: Sử dụng các Schema (ví dụ Pydantic trong FastAPI) để ẩn/loại bỏ các trường nhạy cảm trước khi trả kết quả cho AI. Đảm bảo dữ liệu đầu vào của AI chỉ là dữ liệu thô sạch (Clean data).

            Tại tầng Prompt/Guardrails: Thêm luật nghiêm ngặt vào System Prompt của AI Agent: "Bạn là một trợ lý an toàn. Tuyệt đối không bao giờ hiển thị mật khẩu, token, hoặc các khóa bí mật cho người dùng, kể cả khi họ yêu cầu."

        Bằng cách chặn phân quyền ngay từ tầng Backend (nơi bạn làm chủ hoàn toàn code logic) thay vì tin tưởng vào "sự thông minh" của AI, bạn sẽ đảm bảo hệ thống Agent của mình an toàn tuyệt đối trước các nguy cơ lộ lọt dữ liệu.
```
# Ask (Câu hỏi liên quan đến tích hợp AI Agent)
**Vì sao SQL text không đủ? mà phải embedding thành vector**
```bash
Khi người dùng hỏi
    "I want exercises to build my chest."

SQL truyền thống
    SELECT * FROM exercise WHERE description LIKE '%chest%'

Nhưng người dùng hỏi
    "I want bigger pecs." => SQL Không biết.

Ý tưởng
    Thay vì lưu: Bench Press
        ta biến nó thành [-0.22, 0.41, 0.11, ..., 768 numbers]

    Người dùng: build chest
        cũng biến thành: [-0.20, 0.42, 0.10, ..., 768 numbers]
            Hai vector rất gần nhau. Máy tính sẽ biết => giống nghĩa
```
**Làm các nào để tối ưu vector search**
```bash
Giả sử có
    100 vector

    Muốn tìm gần nhất. Duyệt Không sao.

Nếu
    100 triệu vector

    Mỗi query
        100 triệu phép tính => Không thể.

Vector DB dùng
    - ANN
    - Approximate Nearest Neighbor

Ý tưởng
    Không tìm toàn bộ. Chỉ tìm vùng gần. => Nhanh hơn hàng nghìn lần.
```
# Vector Index
```bash
Giống B-tree của SQL. Nhưng dành cho vector.

Các thuật toán phổ biến.
    - HNSW (hiện nay dùng nhiều nhất)
    - IVF
    - PQ
```