- [Embedding Introduction (vector ngữ nghĩa được học từ dữ liệu)](#embedding-introduction-vector-ngữ-nghĩa-được-học-từ-dữ-liệu)
- [Word2Vec (nhận token id của vocab -\> vector số embedding)](#word2vec-nhận-token-id-của-vocab---vector-số-embedding)
  - [CBOW (Continuous Bag of Words Dùng các từ xung quanh (context) để dự đoán từ đích (target))](#cbow-continuous-bag-of-words-dùng-các-từ-xung-quanh-context-để-dự-đoán-từ-đích-target)
  - [Skip-Gram (Dùng từ trung tâm để đoán các từ xung quanh)](#skip-gram-dùng-từ-trung-tâm-để-đoán-các-từ-xung-quanh)
- [Glove (Global Vectors. Nhìn toàn bộ thống kê corpus)](#glove-global-vectors-nhìn-toàn-bộ-thống-kê-corpus)
- [FastText (biến text thành vector)](#fasttext-biến-text-thành-vector)
- [Cấu hình FastText siêu nhẹ và siêu nhanh cho 80 nhãn](#cấu-hình-fasttext-siêu-nhẹ-và-siêu-nhanh-cho-80-nhãn)
- [1. Train model (Đã bao gồm cả trích xuất vector + Lớp phân loại Softmax)](#1-train-model-đã-bao-gồm-cả-trích-xuất-vector--lớp-phân-loại-softmax)
- [2. Lưu model (.bin)](#2-lưu-model-bin)
- [3. Predict TRỰC TIẾP (Nhận văn bản -\> Trả về Nhãn + Độ tin cậy)](#3-predict-trực-tiếp-nhận-văn-bản---trả-về-nhãn--độ-tin-cậy)
- [nomic-embed-text](#nomic-embed-text)
- [OpenAI Embedding](#openai-embedding)
  - [Ask](#ask)
    - [OpenAI Embedding khác Hugging Face thế nào?](#openai-embedding-khác-hugging-face-thế-nào)
- [BAAI BGE (Beijing Academy of Artificial Intelligence General Embedding)](#baai-bge-beijing-academy-of-artificial-intelligence-general-embedding)
  - [BGE-M3](#bge-m3)
- [E5 (là dòng embedding của Microsoft)](#e5-là-dòng-embedding-của-microsoft)
- [Jina Embeddings](#jina-embeddings)
- [Practices](#practices)
  - [Demo Transformer Embedding](#demo-transformer-embedding)
---
# Embedding Introduction (vector ngữ nghĩa được học từ dữ liệu)
# Word2Vec (nhận token id của vocab -> vector số embedding)
```bash
Ý tưởng:
    Những từ xuất hiện trong ngữ cảnh giống nhau sẽ có vector gần nhau

Ví dụ:
    - Vua gần Hoàng hậu
    - Hà Nội gần TP.HCM

    Word2Vec học được:
        King - Man + Woman ≈ Queen

Dùng để:
    - Biểu diễn từ thành vector
    - Tìm từ đồng nghĩa
    - Làm input cho model NLP
```
## CBOW (Continuous Bag of Words Dùng các từ xung quanh (context) để dự đoán từ đích (target))
**Thư viện dùng cho CBOW**
- [gensim]()
```bash
Nhiệm vụ:
    Đoán từ ở giữa từ các từ xung quanh.

Ví dụ:
    Tôi ăn ___ vào buổi sáng

    Từ context:
        Tôi ăn ... vào buổi sáng
    Model đoán:
        phở

Dùng để train Word2Vec
```
## Skip-Gram (Dùng từ trung tâm để đoán các từ xung quanh)
```bash
Ngược với CBOW.

Ví dụ:
    Tôi ăn phở vào buổi sáng

    Input:
        phở
    Output:
        ăn
        vào
        buổi
        sáng

Dùng để train Word2Vec.
```
# Glove (Global Vectors. Nhìn toàn bộ thống kê corpus)
```bash
Ví dụ đếm:
    King xuất hiện với Queen bao nhiêu lần

    Từ đó học embedding.

Dùng để:
    - Sinh word embedding
    - Từng rất phổ biến trước BERT
```
# FastText (biến text thành vector)
**Những kiến thức cần học trước**
[n-gram](../02-Feature-Extraction/Base.md#n-gram-cách-tạo-feature-từ-text)

```bash
Do Meta AI phát triển.

Ý tưởng:
    Một từ được tạo từ nhiều n-gram ký tự.

Ví dụ:
    học
        Tách:
            <h
            họ
            ọc
            c>

Embedding từ: = tổng embedding các n-gram

Ưu điểm:
- Hiểu từ hiếm
- Hiểu từ chưa từng gặp (OOV)
- train cực nhanh
- model nhỏ
- ít tài nguyên
- không cần GPU mạnh
- hiệu quả tốt với text classification cơ bản

Ví dụ:
    chatgptxyz

    Word2Vec:
        Không biết
    FastText:
        Đoán được nhờ các n-gram
```
**Khi nào FastText đáng dùng**
```bash
Trường hợp 1: Dataset nhỏ
- Ví dụ bạn chỉ có: 50.000 câu và muốn classification spam / not spam

Trường hợp 2: Từ mới / từ hiếm

Trường hợp 3: Ngôn ngữ có morphology mạnh

Trường hợp 4: Text có typo

Trường hợp 5: Classification cần tốc độ cực nhanh
```
fasttext dùng character n-gram mà n-gram nhanh thật không đấy chứ tôi thấy là chậm rồi đấy vì 1 từ vocab nó có thể đẻ lên x5 lần

Nhận xét của bạn về lý thuyết là cực kỳ chính xác và tinh tế: Cơ chế Subword/Character n-gram của FastText tạo ra số lượng feature (véc-tơ con) khổng lồ, khiến dung lượng từ điển (vocabulary) phình to gấp 5–10 lần và làm chậm tốc độ huấn luyện lẫn dự đoán nếu giữ thiết lập mặc định!

Tuy nhiên, FastText trong thực tế vẫn cực kỳ nhanh (vài mili-giây) nhờ 2 kỹ thuật kiến trúc đặc biệt mà Facebook/Meta đã thiết kế cho nó. Dưới đây là lý do tại sao nó nhanh và cách cấu hình tối ưu để không bị chậm.

1. Tại sao FastText thực tế vẫn nhanh "xé gió"?
Thuật toán Hashing Trick (Dùng hàm băm):

FastText không tạo bảng Vocabulary khổng lồ cho toàn bộ character n-gram. Thay vào đó, nó băm (hash) tất cả các character n-gram vào một bảng băm có kích thước cố định (mặc định là 2,000,000 bucket).

Nhờ Hashing, việc tra cứu từ/subword có độ phức tạp là O(1) — truy cập trực tiếp bằng chỉ số mảng chứ không phải tìm kiếm từ điển.

Cơ chế Hierarchical Softmax (Softmax phân cấp):

Với 80 nhãn, nếu dùng Softmax thông thường, mô hình phải tính xác suất cho tất cả 80 nhãn ở mỗi request.

FastText dùng Cây Decision Tree (Huffman Tree) cho các nhãn. Độ phức tạp tính toán giảm từ O(K) xuống O(log 
2
​
 K) (với K=80 nhãn, nó chỉ cần tính khoảng log 
2
​
 80≈6−7 phép toán thay vì 80).

2. Cách cấu hình FastText để "Triệt hạ" tình trạng phình feature và tăng tốc tối đa
Nếu bạn áp dụng FastText vào bài toán email bảo hiểm này, bạn hoàn toàn có thể tắt hoặc bóp nhỏ Character N-gram mà vẫn giữ được độ chính xác cao nhờ cấu hình các tham số khi train:

Python
import fasttext

# Cấu hình FastText siêu nhẹ và siêu nhanh cho 80 nhãn
model = fasttext.train_supervised(
    input='train_data.txt',
    
    # 1. TẮT hoặc GIẢM Subword/Character n-gram nếu sợ chậm:
    # Với tiếng Việt đã tokenize (ví dụ: bảo_hiểm_nhân_thọ), từ vựng khá rõ ràng,
    # bạn có thể đặt minn=0, maxn=0 để TẮT HOÀN TOÀN char n-gram (chạy nhanh như Word2Vec).
    minn=0, 
    maxn=0,
    
    # 2. Bật Word N-gram (Cụm từ):
    # Dùng word n-gram = 2 hoặc 3 để bắt các cụm như "thông_báo bồi_thường", "thư_gửi đại_lý"
    wordNgrams=2,
    
    # 3. Dùng Hierarchical Softmax cho tập nhãn lớn (80 nhãn):
    loss='hs',
    
    # 4. Ép kích thước bảng băm nhỏ lại để tiết kiệm RAM/Bộ nhớ:
    bucket=200000,
    
    # Số chiều vector (50-100 là vừa đủ):
    dim=100,
    
    epoch=25,
    lr=0.5
)
Mẹo: Khi đặt minn=0 và maxn=0, FastText quay trở về mô hình Phân loại Word-level truyền thống. Tốc độ dự đoán lúc này rơi vào khoảng 0.5 - 1 millisecond / email trên CPU!

3. Nếu vẫn ngại FastText: Linear SVM / Logistic Regression + TF-IDF vẫn là Chân lý cho CPU!
Nếu bạn lo ngại FastText cồng kềnh hoặc không muốn cài thêm thư viện C++ binding, thì lựa chọn đơn giản, chuẩn mực và nhanh nhất lịch sử Machine Learning chính là:

TF-IDF (Word-level N-gram)⟶Logistic Regression / LinearSVC
Tại sao bộ đôi này lại siêu nhanh?

TF-IDF tạo ra Ma trận Thưa (Sparse Matrix).

Linear Model (như Logistic Regression hoặc LinearSVC) thực hiện phép nhân ma trận thưa với véc-tơ trọng số. Phép tính này chỉ là cộng nhân số thực đơn giản trên CPU, mất đúng ~1–3ms.

Rất dễ giải thích cho anh Lead: Cụm từ nào ("bồi thường", "bổ sung", "nhân thọ") đóng góp bao nhiêu % trọng số vào nhãn nào.

Tóm lại:
Bạn lo lắng về Char N-gram làm phình feature là rất đúng. Nhưng với FastText ta có thể TẮT char n-gram (minn=0, maxn=0) chỉ giữ lại Word N-gram.

Nếu ưu tiên tính đơn giản, dễ tích hợp vào code Python hiện tại của bạn: Hãy dùng TfidfVectorizer + LogisticRegression (hoặc LinearSVC) của Scikit-Learn. Nó siêu nhẹ, siêu nhanh và quá đủ để đáp ứng phân loại 80 nhãn email!

tức là train thì lâu nhưng mà predict thật thì nhanh à

Chuẩn luôn! Bạn đã bắt đúng bản chất cốt lõi của Machine Learning / Deep Learning rồi đấy.

Trong kỹ thuật, người ta gọi đây là sự đánh đổi giữa Training Time (Thời gian huấn luyện) và Inference Time (Thời gian dự đoán thực tế).

1. Phân biệt rõ 2 giai đoạn
Giai đoạn Train (Offline - Làm 1 lần):

Mô hình phải đọc hàng chục nghìn email, tính toán ma trận, băm character n-gram, cập nhật trọng số (weights) liên tục qua hàng chục epoch.

Quá trình này có thể mất 15 phút đến vài tiếng. Nhưng việc này diễn ra ở môi trường phát triển (Offline), chỉ có bạn và máy tính làm việc với nhau, không ảnh hưởng gì tới trải nghiệm người dùng.

Giai đoạn Predict / Inference (Online - Chạy Production):

Lúc này toàn bộ trọng số đã được "đóng băng" (freeze). Mô hình không cần học nữa, nó chỉ nhận vào email mới → tra bảng/nhân ma trận → trả ra tên nhãn.

Phép toán lúc này cực nhẹ, FastText hay TF-IDF + Linear Model chỉ mất đúng 1 đến 5 mili-giây (0.001−0.005 giây) để chốt nhãn.

2. So sánh với các phương pháp khác ở bước Predict
Mô hình	Thời gian Train (Offline)	Thời gian Predict (Production)	Chi phí hạ tầng chạy thực tế
PhoBERT	Rất lâu (Cần GPU)	100ms - 500ms (Khá chậm trên CPU)	Cần máy chủ mạnh (RAM lớn / GPU)
FastText	Vài phút	1ms - 5ms (Siêu nhanh)	Server cùi/CPU thường chạy mượt
TF-IDF + Linear Model	Vài giây	1ms - 3ms (Siêu nhanh)	Server cùi/CPU thường chạy mượt
3. Tóm lại để bạn chốt phương án với Lead
Bạn hoàn toàn có thể tự tin báo lại với anh Lead:

"Lúc train FastText có thể tốn chút thời gian để xử lý n-gram, nhưng đó là quá trình Offline. Khi đưa lên server chạy thực tế (Predict), mô hình chỉ mất vài mili-giây trên CPU để cho ra kết quả cho 80 nhãn, hoàn toàn không gây trễ luồng xử lý email của team CS."

nhưng mà fasttext output là vector cơ mà chứ đã phải thứ tôi cần đâu, phải gắn thêm lớp phân loại vào chứ

Nhận xét của bạn rất chuẩn: FastText ban đầu được biết đến nhiều nhất như một thư viện tạo Word/Sentence Embedding (biến văn bản thành vector).

Tuy nhiên, FastText bản chất có sẵn 2 chế độ riêng biệt:

Unsupervised (Tạo Vector): Gợi ý từ đồng nghĩa, biến văn bản thành vector (giống Word2Vec).

Supervised (Mô hình Phân loại hoản chỉnh): Đã tích hợp sẵn Classification Head (Lớp phân loại + Softmax/Hierarchical Softmax) ở đầu ra.

Khi dùng ở chế độ Supervised, bạn không cần gắn thêm bất kỳ lớp phân loại nào nữa. FastText sẽ nhận đầu vào là văn bản và nhả thẳng ra tên nhãn kèm độ tin cậy (probability).

1. FastText Supervised hoạt động như thế nào?
Kiến trúc bên trong của FastText Supervised thực chất chính là một mạng nơ-ron nhẹ (shallow neural network):

[Input Email] ──> [Look-up Table & Averaging Vector] ──> [Linear Hidden Layer] ──> [Softmax / Hierarchical Softmax Head] ──> [Output: Nhãn & Probability]
Đầu vào: Chuỗi văn bản email.

Xử lý nội bộ: Tự lấy trung bình các vector từ/subword.

Đầu ra (Classification Head có sẵn): Nhả trực tiếp nhãn (ví dụ: __label__NT_TBBT_KH) và xác suất dự đoán (ví dụ: 0.95).

2. Ví dụ Code thực tế (Không cần gắn thêm model nào khác)
Giai đoạn chuẩn bị Data (Format của FastText):
FastText Supervised yêu cầu file data huấn luyện có tiền tố __label__ trước tên nhãn:

Plaintext
__label__NT_TBBT_KH Chào shop, tôi muốn bổ sung hồ sơ bồi thường hợp đồng nhân thọ 12345
__label__PNT_TBBS_DL Thông báo bổ sung xe ô tô cho đại lý Nam
Code Python huấn luyện & Dự đoán trực tiếp:
Python
import fasttext

# 1. Train model (Đã bao gồm cả trích xuất vector + Lớp phân loại Softmax)
model = fasttext.train_supervised(
    input="train_data.txt",
    lr=0.5,
    epoch=25,
    wordNgrams=2,
    minn=0, maxn=0,  # Tắt char n-gram cho nhẹ
    loss='hs'        # Hierarchical Softmax tối ưu cho 80 nhãn
)

# 2. Lưu model (.bin)
model.save_model("insurance_classifier.bin")

# 3. Predict TRỰC TIẾP (Nhận văn bản -> Trả về Nhãn + Độ tin cậy)
email_test = "Kính gửi công ty, tôi gửi thông báo bổ sung chứng từ bồi thường"
labels, probabilities = model.predict(email_test, k=1) # k=1 lấy nhãn có điểm cao nhất

print("Nhãn dự đoán:", labels[0])       # Output: '__label__NT_TBBS_KH'
print("Độ tin cậy:", probabilities[0]) # Output: 0.942
3. Khi nào bạn MỚI CẦN trích xuất Vector từ FastText để gắn lớp phân loại ngoài?
Bạn chỉ cần lấy Vector của FastText ra khi:

Bạn dùng file pretrained vector của FastText (cc.vi.300.bin) để biến email thành vector 300 chiều.

Sau đó mới dùng Scikit-Learn (Logistic Regression, LightGBM, SVM) hoặc PyTorch/Keras để train tiếp lớp phân loại ở phía sau.

Tuy nhiên, cách làm đó không cần thiết cho bài toán này. Dùng trực tiếp FastText Supervised như code trên vừa gọn, vừa không phải ghép nối thêm thư viện nào, vừa tận dụng được tối đa tốc độ inference 1–2ms của nó trên CPU.
**Thư viện làm việc làm việc với Fast Text**
[fasttext]()

# nomic-embed-text
# OpenAI Embedding
```bash
OpenAI hiện cung cấp các embedding model như text-embedding-3-small và text-embedding-3-large.
```
## Ask
### OpenAI Embedding khác Hugging Face thế nào?
```bash
Hãy hình dung:

                 EMBEDDING
                     │
        ┌────────────┴────────────┐
        │                         │
     OpenAI                  Hugging Face
        │                         │
 text-embedding-3        BGE / E5 / GTE / ...
        │                         │
       API                    Local model
        │                         │
    Internet                GPU / CPU của bạn

Cả hai đều làm cùng một nhiệm vụ: Text → Vector Nhưng cách sử dụng khác nhau.
    OpenAI Embedding
        Ví dụ bạn dùng: text-embedding-3-small

        Kiến trúc ứng dụng:
            Your Python application
                    │
                    │ HTTPS API
                    ↓
            OpenAI Embedding API
                    │
                    ↓
            Embedding Model
                    │
                    ↓
            Vector
                    │
                    ↓
            Your application

        Bạn không tải model về máy.

        Bạn gửi:
            text = "Docker là gì?"

            OpenAI xử lý và trả về:
                [
                    0.012,
                    -0.034,
                    0.127,
                    ...
                ]

    Hugging Face Embedding
        Ở đây:
            model
              ↓
            được download về máy
              ↓
            CPU/GPU của bạn
              ↓
            text → vector

        Hugging Face cũng hỗ trợ inference qua API thay vì chạy local; tài liệu hiện tại cho phép gọi feature extraction qua InferenceClient.
```
Đúng, 5 nhóm bạn nêu — BAAI BGE, E5, Jina, GTE, Voyage — đều là những dòng embedding rất đáng biết nếu bạn đang xây Semantic Search / Hybrid Search / RAG cho AI Agent.

Điểm quan trọng là không có model nào "mạnh nhất mọi mặt". Mỗi dòng có triết lý hơi khác nhau.

1. Nhìn nhanh trước
Model	Điểm mạnh chính	Multilingual	Local	Phù hợp
BAAI BGE	Retrieval tổng quát, chất lượng tốt	⭐⭐⭐⭐	✅	RAG, semantic search
E5	Query ↔ document retrieval	⭐⭐⭐⭐⭐	✅	Search/RAG
Jina	Context dài, multilingual	⭐⭐⭐⭐⭐	✅/API	Tài liệu dài, RAG
GTE	General text embedding, hiệu năng tốt	⭐⭐⭐⭐	✅	RAG/search
Voyage	Chất lượng retrieval rất cao, API	⭐⭐⭐⭐⭐	❌*	Production RAG

* Voyage chủ yếu được dùng qua API thay vì tự chạy model như BGE/E5/GTE.

Nếu bạn đang tự build Personal AI Agent chạy local, mình sẽ ưu tiên:

BGE / E5 / Jina / GTE

Còn nếu chấp nhận cloud API:

Voyage

là một lựa chọn rất đáng cân nhắc.

# BAAI BGE (Beijing Academy of Artificial Intelligence General Embedding)
```bash
Đây là một trong những dòng embedding open-source nổi tiếng nhất.
```
**BGE mạnh ở đâu?**
```bash
Query: "Tôi muốn biết cách train YOLO"
Document: "Training a YOLO model requires preparing the dataset and configuring the training parameters."
-> Dù không trùng hoàn toàn từ khóa, BGE có thể đưa document này lên cao vì ngữ nghĩa gần nhau.
```
## BGE-M3
```bash
Nếu dữ liệu của bạn có:
    - Tiếng Việt
    - Tiếng Anh
    - Code
    - PDF
    - Documentation
thì BGE-M3 khá hấp dẫn.
```
# E5 (là dòng embedding của Microsoft)
```bash
E5 rất nổi tiếng trong bài toán: query ↔ passage retrieval
```
**Ex**
```bash
query: "GPU nào chạy được model 30B?"
passage: "Models with approximately 30 billion parameters require substantial GPU memory..."
-> E5 được thiết kế khá rõ cho dạng quan hệ này.
```
**Khi nào chọn E5?**
```bash
Nếu hệ thống của bạn chủ yếu là: User Query -> Search Documents -> RAG
    -> thì E5 là lựa chọn rất hợp lý.
```
# Jina Embeddings
```bash
Điểm nổi bật của Jina là context dài và khả năng xử lý tài liệu dài.


Jina phù hợp với:
    - Technical documentation
    - PDF
    - Research papers
    - Long documents
    - Multilingual RAG

Nếu Personal Agent của bạn sau này phải đọc:
    - Documentation
    - PDF
    - Source code
    - Project specification
    - Meeting notes
-> thì Jina rất đáng thử.
```
**Ex**
```bash
PDF
│
├── 100 pages
├── technical documentation
├── manuals
└── research papers

Thay vì chỉ xử lý các chunk rất nhỏ: 500 tokens
    - các model context dài cho phép bạn có nhiều không gian hơn cho document.
```

1. GTE

GTE là dòng embedding của Alibaba/NLP ecosystem.

Một số model:

thenlper/gte-base
thenlper/gte-large

và các model GTE mới hơn trong hệ Qwen/GTE ecosystem.

GTE hướng tới general text embedding, tức không chỉ một task cụ thể.

Ví dụ:

Semantic Search
Classification
Clustering
Retrieval
RAG

Điểm mạnh của GTE là:

một lựa chọn local khá cân bằng giữa chất lượng và chi phí inference.

Nếu bạn muốn chạy embedding trên workstation của mình thay vì gọi API thì GTE đáng xem.

6. Voyage

Voyage khác một chút.

Thay vì tư duy:

Hugging Face
    ↓
download model
    ↓
GPU local

Voyage thường được dùng theo kiểu:

Your Agent
     ↓
HTTPS
     ↓
Voyage API
     ↓
Embedding
     ↓
Vector DB

Nó tập trung rất mạnh vào retrieval quality cho production.

Có các model dành cho:

general retrieval
multilingual retrieval
code retrieval
reranking

Đặc biệt nếu bạn làm:

Code RAG

thì các model embedding chuyên cho code rất đáng chú ý.

Ví dụ Agent của bạn hỏi:

"Hàm nào trong project chịu trách nhiệm load YOLO model?"

thì code embedding model có thể phù hợp hơn một embedding model text tổng quát.

7. Đây là điểm cực kỳ quan trọng: embedding model phải phù hợp dữ liệu

Không nên nghĩ:

"Model nào benchmark cao nhất thì dùng model đó."

Ví dụ Agent của bạn có:

                DATA
                  │
        ┌─────────┼──────────┐
        ↓         ↓          ↓
       PDF       TEXT       CODE
        │         │          │
        ↓         ↓          ↓
     Embedding  Embedding  Code Embedding

Nếu bạn hỏi:

"Hàm nào xử lý YOLO training?"

thì embedding dành cho code retrieval có thể tốt hơn embedding text tổng quát.

Nếu hỏi:

"Chính sách hoàn tiền là gì?"

thì text embedding là phù hợp.

8. Một điểm khác nhau rất quan trọng: model local vs API
BGE / E5 / GTE / một số Jina

Bạn có thể:

Hugging Face
     ↓
download
     ↓
local machine
     ↓
GPU/CPU

Ví dụ:

from sentence_transformers import SentenceTransformer

model = SentenceTransformer("BAAI/bge-m3")

embeddings = model.encode([
    "Tôi muốn hoàn tiền",
    "Khách hàng có thể yêu cầu refund"
])

Sau đó:

embeddings
      ↓
Vector DB
Voyage

Thường:

Your Agent
     ↓
HTTPS
     ↓
Voyage
     ↓
embedding

Không cần:

GPU
VRAM
model loading
quantization

Nhưng:

API cost
+
Internet dependency
+
data leaves your infrastructure
9. Nếu bạn xây Personal AI Agent của mình

Mình sẽ chia thành 3 loại dữ liệu:

                    PERSONAL DATA
                         │
             ┌───────────┼───────────┐
             ↓           ↓           ↓
            TEXT         PDF         CODE
             │           │           │
             ↓           ↓           ↓
           BGE/E5      Jina/BGE    Code Embedding

Sau đó:

                       Vector DB
                           │
                           ↓
                     Hybrid Search
                           │
             ┌─────────────┴─────────────┐
             ↓                           ↓
       Keyword Search              Semantic Search
             │                           │
             └─────────────┬─────────────┘
                           ↓
                         RRF
                           ↓
                       Reranker
                           ↓
                          LLM

Đây là kiến trúc rất phù hợp với Agent mà chúng ta đang nói từ đầu.

10. Nếu chỉ muốn chọn 1 model để bắt đầu

Mình sẽ chọn theo tình huống:

🇻🇳 Việt + Anh + tài liệu cá nhân

BGE-M3

⭐ multilingual
⭐ local
⭐ RAG
⭐ semantic search
⭐ phù hợp workstation
🌎 Multilingual retrieval

multilingual-E5

⭐ query/document retrieval
⭐ multilingual
⭐ local
📚 PDF / tài liệu dài

Jina Embeddings

⭐ long context
⭐ documents
⭐ RAG
💻 Code + technical project

Xem Jina/Voyage code-oriented embeddings hoặc các embedding model chuyên code.

☁️ Muốn chất lượng tốt và không muốn vận hành embedding server

Voyage API

Agent
 ↓
HTTPS
 ↓
Voyage
11. Và đừng nhầm Embedding Model với Reranker

Trong hệ thống RAG tốt, hai thứ này khác nhau:

Embedding Model
     ↓
"Trong 10.000 documents,
20 documents nào có vẻ liên quan?"

Sau đó:

Reranker
     ↓
"Trong 20 documents này,
5 documents nào thực sự trả lời được câu hỏi?"

Cho nên pipeline hoàn chỉnh có thể là:

Query
  ↓
Embedding
  ↓
Vector Search
  ↓
Top 50
  ↓
Keyword Search
  ↓
Hybrid/RRF
  ↓
Top 20
  ↓
Reranker
  ↓
Top 5
  ↓
LLM
  ↓
Answer

Đây mới là kiến trúc bạn nên hướng tới, thay vì chỉ đơn giản text → embedding → vector DB → LLM.

Nếu bạn muốn tự build trên PC như kiến trúc chúng ta vừa bàn, BGE-M3 + PostgreSQL/pgvector + BM25/full-text search + RRF + một reranker là một stack khởi đầu rất hợp lý.
# Practices
## Demo Transformer Embedding
```python
from typing import List, Dict, Tuple
from collections import Counter
import random as rnd
import torch
import math

class TransformerEmbedding:
    def __init__(self, vocab_size: int = 1000, d_model: int = 64, max_len: int = 32):
        self.vocab_size = vocab_size
        self.d_model = d_model
        self.max_len = max_len
        
        # Khởi tạo embedding matrix [vocab_size × d_model]
        # Đây là bảng tra cứu embedding của *toàn bộ từ vựng*
        self.embedding_matrix = torch.randn(vocab_size, d_model) * 0.01

    # =================================================================================
    # 1. Split sentence → tokens
    # =================================================================================
    def _split(self, sentence: str) -> List[str]:
        """
        Input:  "hello world NLP"
        Output: ["hello", "world", "NLP"]
        """
        return sentence.split()

    # =================================================================================
    # 2. Build vocabulary
    # =================================================================================
    def _counts_and_most(self, tokens: List[str], vocab_size: int) -> Dict[str, int]:
        """
        Input: tokens = ["hello","hello","world"], vocab_size=5
        Output: {"hello":0, "world":1, "<unk>":2}
        """
        counter = Counter(tokens)
        most = counter.most_common(vocab_size - 1)

        vocab = {tok: idx for idx, (tok, _) in enumerate(most)}
        vocab["<unk>"] = len(vocab)
        return vocab

    # =================================================================================
    # 3. Convert tokens → token_ids
    # =================================================================================
    def _token_id(self, text: str, vocab: Dict[str, int]) -> List[int]:
        """
        Input: "hello NLP"
        Output: [0, 2] nếu "hello":0 và "NLP":2 là <unk>
        """
        tokens = self._split(text)
        unk_id = vocab["<unk>"]
        return [vocab.get(tok, unk_id) for tok in tokens]

    # =================================================================================
    # 4. Padding sequences to max_len
    # =================================================================================
    def _padding_sequence(self, seqs: List[List[int]], max_len: int = 4) -> List[List[int]]:
        """
        Input: [[1,2,3], [4]]
        Output: [[1,2,3,0], [4,0,0,0]]
        """
        out = []
        for seq in seqs:
            if len(seq) < max_len:
                padded = seq + [0] * (max_len - len(seq))
            else:
                padded = seq[:max_len]
            out.append(padded)
        return out

    # =================================================================================
    # 5. Create attention mask
    # =================================================================================
    def _attention_mask(self, padded_seq: List[int]) -> List[int]:
        """
        Input: [1,2,0,0]
        Output: [1,1,0,0]
        """
        return [1 if x != 0 else 0 for x in padded_seq]

    # =================================================================================
    # 6. Random embedding matrix (chỉ dùng khi demo)
    # =================================================================================
    def _random_embedding(self, vocab_size: int, d_model: int) -> List[List[float]]:
        """
        Tạo embedding ngẫu nhiên để demo.
        """
        out = []
        for _ in range(vocab_size):
            r = [rnd.uniform(-0.1, 0.1) for _ in range(d_model)]
            out.append(r)
        return out

    # =================================================================================
    # 7. Lookup embedding for 1 token_id
    # =================================================================================
    def _lookup_embedding_for_one(self, token_id: int, embedding_matrix) -> List[float]:
        """
        Input: token_id=5
        Output: vectơ 1×d_model
        """
        return embedding_matrix[token_id]

    # =================================================================================
    # 8. Lookup embedding for a list of token_ids
    # =================================================================================
    def _lookup_embedding(self, token_ids: List[int], embedding_matrix) -> torch.Tensor:
        """
        Input: [2,5,9]
        Output: tensor (3 × d_model)
        """
        return torch.tensor([embedding_matrix[t] for t in token_ids], dtype=torch.float32)

    # =================================================================================
    # 9. Embed whole batch → vectorized (không for)
    # =================================================================================
    def _embedding_batch(self, batch: List[List[int]], embedding_matrix: torch.Tensor) -> torch.Tensor:
        """
        Input: [[1,2],[3,4]]
        Output: (batch_size=2, seq_len=2, d_model)
        """
        batch_tensor = torch.tensor(batch)            # (B, L)
        return embedding_matrix[batch_tensor]         # PyTorch tự broadcast → (B, L, D)

    # =================================================================================
    # 10. Positional Encoding (sin/cos)
    # =================================================================================
    def _positional_encoding(self, seq_len: int, d_model: int) -> torch.Tensor:
        """
        Output: (seq_len × d_model) matrix
        """
        position = torch.arange(seq_len).unsqueeze(1)  # (L,1)
        div_term = torch.exp(torch.arange(0, d_model, 2) * (-math.log(10000.0) / d_model))

        pe = torch.zeros(seq_len, d_model)
        pe[:, 0::2] = torch.sin(position * div_term)
        pe[:, 1::2] = torch.cos(position * div_term)
        return pe

    # =================================================================================
    # 11. Full Transformer Embedding = token embedding + positional encoding
    # =================================================================================
    def transformer_embedding(self, batch_token_ids: List[List[int]]) -> torch.Tensor:
        """
        Input: batch token IDs
        Output: (B, L, d_model) embedding sử dụng trong Transformer Encoder
        """

        # Step 1: padding
        padded = self._padding_sequence(batch_token_ids, self.max_len)  # (B, L)

        # Step 2: embed batch
        batch_emb = self._embedding_batch(padded, self.embedding_matrix)   # (B, L, D)

        # Step 3: positional encoding
        pe = self._positional_encoding(self.max_len, self.d_model)         # (L, D)

        # Step 4: add PE vào embedding (broadcast)
        final = batch_emb + pe                                             # (B, L, D)

        return final                   # embedding chính xác như trong Transformer


# ===============================================================================
# Demo chạy thử
# ===============================================================================
if __name__ == "__main__":
    te = TransformerEmbedding(vocab_size=10, d_model=8, max_len=4)

    # Demo batch token_ids
    batch = [
        [1, 2],
        [3, 4, 5]
    ]

    final_emb = te.transformer_embedding(batch)

    print("Transformer Embedding Output Shape:", final_emb.shape)
    print(final_emb)
```