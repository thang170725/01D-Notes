-- [BoW (Bag of Words - Lấy các token rồi đếm số lần xuất hiện)](#bow-bag-of-words---lấy-các-token-rồi-đếm-số-lần-xuất-hiện)
- [BoW (Bag of Words - Lấy các token rồi đếm số lần xuất hiện)](#bow-bag-of-words---lấy-các-token-rồi-đếm-số-lần-xuất-hiện)
- [TF-IDF (biến token thành feature vector)](#tf-idf-biến-token-thành-feature-vector)
  - [Ask (các câu hỏi liên quan đến TF-IDF)](#ask-các-câu-hỏi-liên-quan-đến-tf-idf)
- [Attention](#attention)
---
# BoW (Bag of Words - Lấy các token rồi đếm số lần xuất hiện)
```bash
Ta đếm từ vì mô hình AI cần số.
    BoW biến văn bản thành vector số bằng cách đếm tần suất từ.

    Nhờ vector đó, các thuật toán học máy mới có thể tính toán và học được.

Nó biến văn bản thành một vector số
    Ví dụ:
        Vocabulary: [tôi, thích, ai, machine]
        
        Câu: "Tôi thích AI"

        BoW: [1, 1, 1, 0]

        Ý nghĩa:
            - tôi     xuất hiện 1 lần
            - thích   xuất hiện 1 lần
            - ai      xuất hiện 1 lần
            - machine xuất hiện 0 lần
        => Đây là vector đặc trưng (feature vector).

Nhược điểm của BoW:
    BoW không hiểu ngữ nghĩa.
        Hai câu:
            - dog bites man
            - man bites dog
        => BoW cho vector giống hệt nhau vì chỉ đếm từ.

    Đó là lý do sau này người ta phát triển:
        - Word2Vec
        - GloVe
        - FastText
        - BERT
        - GPT
    => Các mô hình này học ý nghĩa của từ, không chỉ đếm.
```
**Tại sao vẫn học BoW?**
```bash
Vì nó giúp bạn hiểu nền tảng:
    - Văn bản phải được số hóa trước khi đưa vào mô hình.
    - Feature engineering là gì.
    - Tại sao embedding ra đời.
    - Tại sao transformer tốt hơn BoW.

Có thể xem lịch sử như:
    BoW → TF-IDF → Word2Vec → RNN/LSTM → Transformer (BERT/GPT)
```
**Tại sao phải đếm số lần xuất hiện?**
```bash
Vì tần suất từ thường mang thông tin.

Ví dụ phân loại spam:
    FREE FREE FREE WIN MONEY NOW
        Từ FREE xuất hiện 3 lần.
        
        Nếu chỉ ghi:
            FREE có xuất hiện hay không → 1
                thì mất thông tin.

        Còn BoW:
            FREE → 3 lần
                cho mô hình biết:
                    “Từ này được nhấn mạnh rất mạnh.”

Ví dụ trực quan
    - Câu A: I love this movie
    - Câu B: I love love love this movie
    => Con người cảm thấy câu B tích cực hơn => BoW phản ánh điều đó
```
**Nó liên quan gì đến AI?**
```bash
BoW chính là bước chuyển đổi dữ liệu.

Sau khi có vector số, mô hình mới tính được:
    - xác suất
    - khoảng cách
    - gradient
    - trọng số

Ví dụ với Logistic Regression:
    spam_score = w1x1 + w2x2 + w3*x3 + ...
        - x1 = số lần xuất hiện của “free”
        - x2 = số lần xuất hiện của “money”
=> Nếu không có BoW thì x1, x2, ... không tồn tại.
```
# TF-IDF (biến token thành feature vector)
```bash
Là cách  cho NLP truyền thống. 
    Khác với embedding là cách biến token thành vector ngữ nghĩa cho Deep Learning và LLM.
```
**Workflow của TF-IDF**
```bash
Giả sử chúng ta có một tập dữ liệu gồm 3 câu (3 văn bản) sau:
    - Văn bản 1 (D1): "Tôi thích học AI"
    - Văn bản 2 (D2): "Tôi thích ăn kem"
    - Văn bản 3 (D3): "Học AI rất vui"
Tổng số văn bản trong tập dữ liệu là N = 3.
Chúng ta sẽ tính TF-IDF cho các từ trong Văn bản 1 (D_1).
```
```bash
Bước 1: Tính TF (Term Frequency) của các từ trong Văn bản 1
    TF đo lường mức độ thường xuyên của một từ xuất hiện trong một văn bản cụ thể.

    TF = (Số lần từ xuất hiện trong văn bản) / (Tổng số từ của văn bản đó)
 
    Văn bản 1 có tổng cộng 4 từ: "Tôi", "thích", "học", "AI". Mỗi từ xuất hiện đúng 1 lần.

        Từ trong D1 	Số lần xuất hiện	Tổng số từ trong D1 	TF
        Tôi         	1	                    4	                1/4=0.25
        thích          	1	                    4	                1/4=0.25
        học         	1	                    4	                1/4=0.25
        AI          	1	                    4	                1/4=0.25

Bước 2: Tính IDF (Inverse Document Frequency) của từng từ
    IDF đo lường mức độ "hiếm" hoặc "phổ biến" của một từ trên toàn bộ 3 văn bản. Từ nào xuất hiện ở quá nhiều văn bản 
        Ví dụ như từ "Tôi" thì IDF sẽ thấp vì nó không mang tính đặc trưng.

    IDF=log((Tổng số văn bản (N))/ (Số văn bản có chứa từ đó))
        (Ở đây ta dùng logarit tự nhiên ln hoặc log10)

    - Từ "Tôi": Xuất hiện trong D1 và D2 (2 văn bản) → IDF = log10(3/2) ≈ 0.176
    - Từ "thích": Xuất hiện trong D1 và D2 (2 văn bản) → IDF = log10(3/2) ≈ 0.176
    - Từ "học": Xuất hiện trong D1 và D3 (2 văn bản) → IDF = log10(3/2) ≈ 0.176
    - Từ "AI": Xuất hiện trong D1 và D3 (2 văn bản) → IDF = log10(3/2) ≈ 0.176

Bước 3: Tính TF-IDF cho Văn bản 1
    TF-IDF = TF×IDF

    Từ trong D1 	TF      IDF     TF-IDF
    Tôi         	0.25	0.176	0.044
    thích           0.25	0.176	0.044
    học         	0.25	0.176	0.044
    AI          	0.25	0.176	0.044

    Kết quả thu được là một vector đại diện cho Văn bản 1: [0.044, 0.044, 0.044, 0.044].

📈 Giả định trường hợp thực tế (Khi tập dữ liệu lớn lên)
Trong các bài toán thực tế (hàng nghìn văn bản), những từ mang tính kết nối hoặc đại từ như "Tôi", "và", "là", "những" sẽ xuất hiện ở gần như 100% văn bản.

Nếu áp dụng vào công thức:
    - Từ "Tôi" xuất hiện ở 1000 / 1000 văn bản: IDF=log10(1000/1000)=log10(1)=0.
    - Từ "AI" chỉ xuất hiện ở 10 / 1000 văn bản chuyên ngành: IDF=log10(1000/10)=log10(100)=2.

Khi đó, điểm TF-IDF của từ "Tôi" sẽ bị kéo tuột về 0, còn từ "AI" sẽ có điểm số rất cao. Máy tính sẽ ngay lập tức hiểu rằng: "À, Văn bản 1 này nói về chủ đề AI chứ không phải nói về chủ đề Tôi!".
```
## Ask (các câu hỏi liên quan đến TF-IDF)
**Nhiều bài toán dùng luôn Bow và TF-IDF vào train model chứ không dùng embedding**
```bash
Đúng

Thực ra có 2 nghĩa của từ "embedding/vector".
    Theo nghĩa rộng
        Bất kỳ cách nào biến text thành vector số:
            Text
             ↓
            [1, 0, 3, 0, 5]
        => thì đều có thể gọi là:
            - Text Representation
            - Feature Vector
            - Vector Embedding (nghĩa rộng)

Nhiều bài viết sẽ nói:
    "TF-IDF embedding"
        hoặc
    "Document embedding"
    => Không hoàn toàn sai.

Theo nghĩa ML/Deep Learning hiện đại Khi nói:
    - Embedding Layer
    - Word Embedding
    - Sentence Embedding
    - Text Embedding

    người ta thường ám chỉ:
        Vector được học (learned) từ dữ liệu.

    Ví dụ:
        - Word2Vec
        - GloVe
        - FastText
        - BERT 
        - Embedding
        - Sentence 
        - TransformerOpenAI 
        - EmbeddingGemini 
        - Embedding

Khác biệt cốt lõi
    TF-IDF
        Từ:
            - cat
            - dog
            - tiger
        có thể thành:
            - cat   = [0, 1, 0, 0, 0]
            - dog   = [0, 0, 1, 0, 0]
            - tiger = [0, 0, 0, 1, 0]
        Không có khái niệm:
            - cat gần dog
            - dog giống wolf

    Embedding thực sự
        Ví dụ:
            cat
            ↓
            [0.21, 0.55, -0.12]
            dog
            ↓
            [0.22, 0.58, -0.10]
        
        Hai vector gần nhau.
            Model học được:
                cat ≈ dog
            => về mặt ngữ nghĩa.
```
**Tại sao TF-IDF vẫn train được model?**
```bash
Ví dụ:
    Email
     ↓
    TF-IDF
     ↓
    Logistic Regression
     ↓
    Spam / Not Spam
=> Hoàn toàn ổn.
```
# Attention 
Bahdanau Attention là gì?

Attention đầu tiên nổi tiếng.

Ý tưởng:

Khi dịch máy:

Tôi yêu Việt Nam

→

I love Vietnam

Model không cần nhớ toàn bộ câu.

Mỗi từ output:

nhìn lại các từ input quan trọng

Dùng để:

Machine Translation
Seq2Seq
9. Luong Attention là gì?

Phiên bản tối ưu hơn Bahdanau.

Khác biệt chính:

Bahdanau:

Additive Attention

Luong:

Multiplicative Attention

Nhanh hơn.

10. Attention thuộc nhóm nào?

Không phải:

Tiền xử lý

Không phải:

Embedding

Mà thuộc:

Feature Extraction / Representation Learning

Hay chính xác hơn:

Neural Network Architecture

Nó giúp model:

chọn thông tin quan trọng

trong chuỗi.

11. Dot-Product Attention là gì?

Công thức:

score = Q · K

(Q dot K)

Nếu score lớn:

Hai token liên quan mạnh

Ví dụ:

Tôi ăn phở vì nó ngon

Token:

nó

sẽ attention mạnh tới:

phở
12. Multi-Head Attention là gì?

Một head:

Nhìn 1 kiểu quan hệ

Ví dụ:

Tôi ăn phở vì nó ngon

Head 1:

chủ ngữ

Head 2:

động từ

Head 3:

tham chiếu đại từ
Tại sao phải nhiều head?

Một head:

Nhìn một góc

Nhiều head:

Nhìn nhiều góc cùng lúc

Giống:

8 chuyên gia phân tích

thay vì

1 chuyên gia