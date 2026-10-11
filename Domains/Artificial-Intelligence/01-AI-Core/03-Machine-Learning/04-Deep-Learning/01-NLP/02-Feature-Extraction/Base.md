- [BoW (Bag of Words - Lấy các token rồi đếm số lần xuất hiện)](#bow-bag-of-words---lấy-các-token-rồi-đếm-số-lần-xuất-hiện)
- [TF-IDF (biến token thành feature vector)](#tf-idf-biến-token-thành-feature-vector)
  - [Ask (các câu hỏi liên quan đến TF-IDF)](#ask-các-câu-hỏi-liên-quan-đến-tf-idf)
- [Attention](#attention)
- [N-gram (cách tạo feature từ text bằng cách chia chuỗi ký tự thành các nhóm liên tiếp độ dài N)](#n-gram-cách-tạo-feature-từ-text-bằng-cách-chia-chuỗi-ký-tự-thành-các-nhóm-liên-tiếp-độ-dài-n)
  - [Word N-gram (Chia theo từ)](#word-n-gram-chia-theo-từ)
    - [Unigram (từng token từ riêng lẻ)](#unigram-từng-token-từ-riêng-lẻ)
    - [Bigram (từng cặp từ liên tiếp)](#bigram-từng-cặp-từ-liên-tiếp)
    - [Trigram (bộ 3 từ liên tiếp)](#trigram-bộ-3-từ-liên-tiếp)
  - [Character N-gram (Chia theo ký tự)](#character-n-gram-chia-theo-ký-tự)
  - [Ask](#ask)
    - [Vậy n-gram có phải embedding không?](#vậy-n-gram-có-phải-embedding-không)
    - [N-gram liên quan gì đến FastText?](#n-gram-liên-quan-gì-đến-fasttext)
  - [word n-gram?](#word-n-gram)
    - [Khi nào dùng character n-gram?](#khi-nào-dùng-character-n-gram)
  - [Character n-gram (là kỹ thuật chia một chuỗi văn bản thành các đoạn con liên tiếp dài đúng n ký tự)](#character-n-gram-là-kỹ-thuật-chia-một-chuỗi-văn-bản-thành-các-đoạn-con-liên-tiếp-dài-đúng-n-ký-tự)
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
Là cách cho NLP truyền thống. 
    Khác với embedding là cách biến token thành vector ngữ nghĩa cho Deep Learning và LLM.
```
**Workflow của TF-IDF**
```bash
Giả sử chúng ta có một tập dữ liệu gồm 3 câu (3 văn bản) sau:
    - Văn bản 1 (D1): "Tôi thích học AI"
    - Văn bản 2 (D2): "Tôi thích ăn kem"
    - Văn bản 3 (D3): "Học AI rất vui"
Tổng số văn bản trong tập dữ liệu là N = 3.
Vocab = ["tôi", "thích", "học", "AI", "ăn", "kem", "rất", "vui"]

Chúng ta sẽ tính TF-IDF cho các từ trong Văn bản 1 (D_1).
```
```bash
Bước 1: Tính TF (Term Frequency) của các từ trong Văn bản 1
    TF là đo lường mức độ thường xuyên của một từ xuất hiện trong một văn bản cụ thể.
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

# N-gram (cách tạo feature từ text bằng cách chia chuỗi ký tự thành các nhóm liên tiếp độ dài N)
## Word N-gram (Chia theo từ)
**Ex**
```bash
Tôi muốn yêu cầu bồi thường bảo hiểm.

-> Word 1-gram (Unigram): Mỗi cụm có 1 từ: [Tôi, muốn, yêu_cầu, bồi_thường, bảo_hiểm]
-> Word 2-gram (Bigram): Mỗi cụm có 2 từ liên tiếp. [Tôi muốn, muốn yêu_cầu, yêu_cầu bồi_thường, bồi_thường bảo_hiểm]
-> Word 3-gram (Trigram): Mỗi cụm có 3 từ liên tiếp. [Tôi muốn yêu_cầu, muốn yêu_cầu bồi_thường, yêu_cầu bồi_thường bảo_hiểm]
```
### Unigram (từng token từ riêng lẻ)
### Bigram (từng cặp từ liên tiếp)
### Trigram (bộ 3 từ liên tiếp)

nắm bắt ngữ cảnh cục bộ (ví dụ “New York” là bigram, có ý nghĩa khác so với hai từ riêng). Dùng trong: language modelling, feature cho classification, spelling correction, autocomplete.
    • Ví dụ dễ hiểu (word-level):
        ◦ Câu: “tôi yêu học AI”
        ◦ Unigrams: [“tôi”, “yêu”, “học”, “AI”]
        ◦ Bigrams: [“tôi yêu”, “yêu học”, “học AI”]
    • Ưu: đơn giản, hiệu quả cho nhiều task.
    • Nhược: số lượng feature bùng nổ khi N tăng; cần smoothing cho language model.
```
**Nhược điểm**
```bash
Nếu tăng N quá lớn: unigram, bigram, trigram, 4-gram, 5-gram, ... -> số lượng feature tăng rất nhanh.
    Ví dụ: 100,000 vocabulary -> thì số possible bigram/trigram có thể cực kỳ lớn.

    Vấn đề: n tăng -> feature space tăng -> memory tăng -> sparse matrix rất lớn -> training chậm
```
## Character N-gram (Chia theo ký tự)
2. Character N-gram là gì?
Character N-gram lấy các cụm gồm \(N\) ký tự liên tiếp, thay vì lấy từ.
Ví dụ văn bản:
claim
Nếu dùng Character 3-gram, ta thu được:
Character 3-gram
c

l

a

i

m


cla


lai


aim



Mỗi cụm gồm 3 ký tự liên tiếp.


Nếu dùng Character 4-gram với từ claim, kết quả là:
- clai
- laim
Character N-gram không nhất thiết phải biết đâu là ranh giới từ. Nó chỉ cần chuỗi ký tự.
Điểm mạnh của Character N-gram là có thể nhận diện các mẫu ký tự chung ngay cả khi từ bị viết sai, có biến thể hoặc có định dạng đặc biệt.
Ví dụ trong email:
- claim
- claims
- claimant
- reclaim
Một số cụm ký tự có thể xuất hiện ở nhiều từ khác nhau. Nhờ vậy, mô hình có thể học được những mẫu liên quan đến từ vựng mà không cần coi mỗi từ là một đơn vị hoàn toàn độc lập.
3. So sánh trực tiếp
Tiêu chí	Word N-gram	Character N-gram
Đơn vị xử lý	Từ hoặc token	Ký tự
Nhận diện cụm từ	Tốt	Không trực tiếp bằng word n-gram
Nhạy với lỗi chính tả	Thường nhạy hơn	Thường ít nhạy hơn
Xử lý từ mới	Có thể khó nếu từ chưa có trong từ vựng	Có thể tận dụng các cụm ký tự đã thấy
Số lượng đặc trưng	Có thể lớn	Có thể rất lớn
Chi phí xử lý	Thường thấp hơn khi dùng tokenizer đơn giản	Phụ thuộc độ dài chuỗi và phạm vi n-gram
Phù hợp	Cụm từ, ý nghĩa nghiệp vụ	Biến thể từ, mã, lỗi gõ, mẫu ký tự
4. Với bài toán phân loại email của bạn, nên dùng loại nào?
Tôi đề xuất thử nghiệm ba phương án:

Phương án A — Word N-gram
Baseline
Dùng word unigram và bigram. Phù hợp để nhận biết cụm từ nghiệp vụ, thường là lựa chọn khởi đầu tốt.




Phương án B — Character N-gram
Dùng các cụm ký tự ngắn, chẳng hạn độ dài từ 3 đến 5 ký tự. Hữu ích khi email chứa mã hồ sơ, lỗi gõ, từ viết tắt hoặc nhiều biến thể từ.




Phương án C — Kết hợp cả hai
Kết hợp đặc trưng word n-gram và character n-gram. Có thể cải thiện khả năng phân loại nhưng cũng làm tăng số lượng đặc trưng, dung lượng bộ nhớ và thời gian huấn luyện.



Để hướng đến tốc độ cao, hãy bắt đầu với Word 1–2 gram. Sau đó so sánh với phương án kết hợp Character 3–5 gram trên cùng tập dữ liệu. Chỉ giữ phần character nếu chất lượng phân loại được cải thiện đủ để bù cho chi phí tăng thêm.
Không có phương án nào tự bảo đảm accuracy trên 95%; bạn cần đánh giá trên tập validation và tập test tách biệt.
Một lưu ý quan trọng: N-gram là cách tạo đặc trưng, không phải mô hình phân loại. Sau bước này, các cụm từ hoặc ký tự thường được chuyển thành vector số, ví dụ bằng TF-IDF, rồi mới đưa vào mô hình huấn luyện.

**Khi nào nên dùng n-gram?**
```bash
- Dùng n-gram khi một từ riêng lẻ không đủ thông tin, và bạn muốn giữ một phần context cục bộ.
    Ví dụ: not good
        - Nếu chỉ dùng unigram:
            + not
            + good
            
            Model thấy: good và có thể nghĩ đây là positive.
        - Nhưng nếu dùng bigram: not good
            + thì model có một feature rất mạnh biểu diễn ý nghĩa phủ định.
```
**Ex: Ví dụ sentiment analysis**
```bash
Dataset:
    I love this movie
    I hate this movie
    This movie is not good
    This movie is very good
```
**Ứng dụng**
[FastText](../03-Text-Embedding/Base.md#fasttext-biến-text-thành-vector)

## Ask
### Vậy n-gram có phải embedding không?
```bash
Không nên gọi n-gram là embedding.

N-gram biến: "I love machine learning" -> "I love", "love machine", "machine learning", v.v
    -> Nó tạo ra text units/features.

Embedding: "machine learning" -> [0.12, -0.32, 0.71, ...]
    -> Nó tạo ra dense vector mang thông tin biểu diễn.
```
### N-gram liên quan gì đến FastText?
```bash
N-gram còn có loại character n-gram:
    Ví dụ: playing
        Character n-gram có thể tạo: pla, play, lay, layi, ayin, ying, ing, v.v
            -> FastText dùng những character n-gram này để học representation.

Cho nên:
    N-gram
       │
       ├── word n-gram
       │      └── TF-IDF
       │
       └── character n-gram
              └── FastText
```
## word n-gram?
```bash
Dùng khi cụm từ có ý nghĩa quan trọng.
    Ví dụ: "New York", "machine learning", "credit card", "not good", "very good", "customer service", v.v
        - Unigram: New, York -> không mạnh bằng New York
```
### Khi nào dùng character n-gram?
```bash
Dùng khi bạn quan tâm đến:
    - typo
    - từ hiếm
    - từ mới
    - morphology
    - tên riêng
    - mã sản phẩm
    - URL
    - text không chuẩn

Ví dụ: 
    - iphone, iphon, iphon14, iphone14, v.v -> Character n-gram có thể giúp các từ này có feature chung.
    - hello, helo, helllo, v.v -> Character n-gram có thể nhận ra chúng khá giống nhau.
```
10. Một workflow rất điển hình

Nếu bạn có bài toán:

Phân loại email spam.

Có thể làm:

Email
 ↓
Cleaning
 ↓
Tokenization
 ↓
N-gram
 ↓
TF-IDF
 ↓
Sparse vector
 ↓
Logistic Regression / Linear SVM
 ↓
Spam / Not Spam

Ví dụ:

"Congratulations you won free money"

Bigram:

Congratulations you
you won
won free
free money

Model có thể học:

"free money"       → spam
"won free"         → spam

Điều này thường tốt hơn chỉ nhìn từng từ riêng lẻ.

11. So sánh 4 thứ để bạn khỏi nhầm
Kỹ thuật	Nó làm gì?	Ví dụ
Tokenization	Tách text	"I love NLP" → I, love, NLP
N-gram	Gom token/ký tự liên tiếp	love NLP
TF-IDF	Biến feature thành vector	[0.1, 0.8, ...]
Embedding	Học dense representation	[0.12,-0.32,...]

Và:

                 TEXT
                  │
            Tokenization
                  │
                  ↓
               N-gram
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
     TF-IDF              FastText
        ↓                   ↓
   sparse vector       dense embedding
        │                   │
        └─────────┬─────────┘
                  ↓
               Model
12. Cách chọn cực nhanh

Nếu bài toán của bạn là:

"Tôi cần một baseline NLP đơn giản, nhanh, dễ train"

→ TF-IDF + n-gram + Logistic Regression/SVM

"Tôi muốn giữ phrase như not good, credit card"

→ word n-gram

"Tôi có typo, từ hiếm, từ mới"

→ character n-gram

"Tôi muốn semantic meaning giữa các từ"

→ Word2Vec / FastText / embedding

"Tôi muốn hiểu context sâu của câu"

→ BERT / Transformer

Một cách nhìn rất hay để học NLP là:

                 NLP REPRESENTATION

Bag of Words
     ↓
N-gram
     ↓
TF-IDF
     ↓
Word2Vec
     ↓
FastText
     ↓
RNN/LSTM
     ↓
Transformer
     ↓
BERT/GPT

Ở mỗi bước, bạn đang giải quyết một hạn chế của representation trước đó. Nếu bạn đang học theo hướng muốn hiểu “tại sao người ta phát minh ra model tiếp theo?”, thì chính chuỗi này là một roadmap rất tốt.

Trong kỹ thuật N-gram, 3-gram, 4-gram và 5-gram khác nhau ở số lượng từ liên tiếp được lấy ra để phân tích trong một văn bản.
- 3-gram: Mỗi cụm gồm 3 từ liên tiếp.
- 4-gram: Mỗi cụm gồm 4 từ liên tiếp.
- 5-gram: Mỗi cụm gồm 5 từ liên tiếp.
1. Ví dụ minh họa
Giả sử ta có câu:
Tôi đang học xử lý ngôn ngữ tự nhiên

Câu này có 7 từ:
Tôi | đang | học | xử | lý | ngôn | ngữ | tự | nhiên
Thực tế có 9 từ, và khi áp dụng N-gram, ta thu được kết quả như sau.
3-gram — Cụm 3 từ
Mỗi lần lấy 3 từ liên tiếp, dịch sang phải 1 từ.
1. Tôi đang học
2. đang học xử
3. học xử lý
4. xử lý ngôn
5. lý ngôn ngữ
6. ngôn ngữ tự
7. ngữ tự nhiên

Tổng cộng: 7 cụm


4-gram — Cụm 4 từ
Mỗi lần lấy 4 từ liên tiếp.
1. Tôi đang học xử
2. đang học xử lý
3. học xử lý ngôn
4. xử lý ngôn ngữ
5. lý ngôn ngữ tự
6. ngôn ngữ tự nhiên

Tổng cộng: 6 cụm


5-gram — Cụm 5 từ
Mỗi lần lấy 5 từ liên tiếp.
1. Tôi đang học xử lý
2. đang học xử lý ngôn
3. học xử lý ngôn ngữ
4. xử lý ngôn ngữ tự
5. lý ngôn ngữ tự nhiên

Tổng cộng: 5 cụm


Công thức tính số cụm N-gram trong câu có \(L\) từ, không thêm ký hiệu đầu hoặc cuối câu:
\[
\text{Số cụm} = L-n+1
\]

Với câu có 9 từ:
- 3-gram: \(9-3+1=7\) cụm.
- 4-gram: \(9-4+1=6\) cụm.
- 5-gram: \(9-5+1=5\) cụm.
2. Vậy 3-gram, 4-gram và 5-gram khác nhau ở điểm nào?
Tiêu chí	3-gram	4-gram	5-gram
Số từ trong mỗi cụm	3	4	5
Ngữ cảnh được xem xét	Ngắn hơn	Trung bình	Dài hơn
Số cụm tạo ra từ cùng một câu	Nhiều hơn	Ít hơn	Ít nhất
Khả năng ghi nhận cụm từ dài	Thấp hơn	Tốt hơn	Tốt hơn nữa
Nguy cơ gặp cụm chưa từng xuất hiện khi huấn luyện	Thấp hơn tương đối	Cao hơn	Cao hơn nữa
3. Ví dụ ứng dụng trong dự đoán từ tiếp theo
Giả sử câu cần dự đoán là:
Hôm nay tôi muốn uống ...

Nếu dùng N-gram để dự đoán từ tiếp theo:
- 3-gram: Dựa vào 2 từ trước đó, chẳng hạn muốn uống, để dự đoán từ tiếp theo.
- 4-gram: Dựa vào 3 từ trước đó, chẳng hạn tôi muốn uống.
- 5-gram: Dựa vào 4 từ trước đó, chẳng hạn nay tôi muốn uống.
Ví dụ, mô hình có thể dự đoán từ tiếp theo là nước, cà phê hoặc trà, tùy theo xác suất học được từ dữ liệu.
Điểm quan trọng là mô hình N-gram bậc \(n\) thường dự đoán từ tiếp theo dựa trên tối đa \(n-1\) từ đứng trước nó.
4. Khi nào nên dùng loại nào?
- 3-gram: Phù hợp khi dữ liệu huấn luyện không quá lớn, cần mô hình đơn giản.
- 4-gram: Cân bằng giữa độ dài ngữ cảnh và lượng dữ liệu cần thiết.
- 5-gram: Hữu ích khi cần xét ngữ cảnh dài hơn và có đủ dữ liệu huấn luyện.
Lưu ý: N-gram bậc cao không phải lúc nào cũng tốt hơn. Chẳng hạn, nếu cụm 5 từ xuất hiện rất ít trong dữ liệu, mô hình có thể không ước lượng được xác suất đáng tin cậy.
Tóm lại: Số đứng trước gram chính là số từ trong mỗi cụm. N càng lớn thì ngữ cảnh càng dài, nhưng mô hình thường cần nhiều dữ liệu hơn để học hiệu quả.

nhưng có nên dùng stop word trước n-gram không vì tôi nghĩ nếu dùng stop word là mình bị cắt mất chữ rồi

Bạn nghĩ như vậy là có lý. Không phải lúc nào cũng nên loại bỏ stop words trước khi áp dụng N-gram. Việc có nên loại bỏ hay không phụ thuộc vào mục đích xử lý văn bản.
Đặc biệt, nếu bạn đang dùng N-gram để phân tích ngôn ngữ hoặc trích xuất cụm từ thì loại bỏ stop words có thể làm mất ngữ cảnh và khiến các cụm từ bị sai ý nghĩa.
1. Ví dụ: Điều gì xảy ra khi loại bỏ stop words trước N-gram?
Giả sử câu tiếng Việt:
Tôi không muốn mua bảo hiểm này.

Giả sử ta coi tôi, không, muốn, này là các từ cần loại bỏ trong một danh sách stop words minh họa.
Cách 1: Giữ nguyên stop words
Văn bản gốc được giữ nguyên.
Tôi | không | muốn | mua | bảo | hiểm | này

Một số 3-gram:
- Tôi không muốn
- không muốn mua
- muốn mua bảo
- mua bảo hiểm
- bảo hiểm này


Cách 2: Loại bỏ stop words trước
Sau khi loại bỏ các từ đã chọn:
mua | bảo | hiểm

Các 3-gram:
- mua bảo hiểm


Bạn thấy vấn đề chưa?
- Từ không mang ý nghĩa phủ định. Nếu xóa nó, câu không muốn mua bảo hiểm có thể bị hiểu sai thành muốn mua bảo hiểm.
- Khi xóa từ, các từ vốn không đứng cạnh nhau trong câu gốc có thể trở thành hàng xóm của nhau, tạo ra N-gram không phản ánh đúng cấu trúc ban đầu.
Lưu ý: Danh sách stop words trên chỉ nhằm minh họa, không có nghĩa tất cả các từ đó đều phải loại bỏ trong mọi bài toán tiếng Việt.
2. Vậy nên dùng stop words trước hay sau N-gram?
Mục đích	Cách xử lý nên cân nhắc
Phân tích cảm xúc, phủ định	Giữ các từ như không, chưa, chẳng
Trích xuất cụm từ, phân tích ngôn ngữ	Thường tạo N-gram trên văn bản đã chuẩn hóa nhưng chưa xóa stop words
Tìm kiếm văn bản	Có thể loại bỏ một số stop words, tùy cách lập chỉ mục và truy vấn
Phân loại văn bản bằng Bag-of-Words hoặc TF-IDF	Có thể thử cả hai cách rồi đánh giá kết quả
Xây dựng mô hình ngôn ngữ N-gram	Thông thường giữ nguyên các từ trong câu để học xác suất từ tiếp theo
3. Nếu muốn giảm nhiễu thì làm thế nào?
Thay vì xóa stop words một cách máy móc, bạn có thể thực hiện quy trình:
Văn bản gốc

Chuẩn hóa văn bản, dấu câu và khoảng trắng
Tách từ phù hợp với ngôn ngữ
Tạo N-gram
Lọc các N-gram không hữu ích theo mục tiêu

Cách này cho phép bạn giữ nguyên ý nghĩa của câu khi tạo N-gram, sau đó mới chọn những cụm từ phù hợp với bài toán.
4. Một điểm quan trọng nếu bạn xử lý tiếng Việt
Tiếng Việt có những từ gồm nhiều tiếng, ví dụ bảo hiểm, ngôn ngữ, xử lý. Nếu chỉ tách theo khoảng trắng, hệ thống sẽ coi mỗi tiếng là một token riêng.
Vì vậy, nếu bạn muốn khai thác N-gram để trích xuất cụm từ tiếng Việt, hãy cân nhắc tách từ tiếng Việt trước khi tạo N-gram. Nếu không, các cụm 3-gram, 4-gram có thể không tương ứng với ba hoặc bốn từ theo nghĩa ngôn ngữ học.
Kết luận: Với bài toán trích xuất cụm từ hoặc mô hình hóa ngôn ngữ, tôi khuyên bạn nên bắt đầu bằng cách giữ stop words, tạo N-gram trước, rồi đánh giá xem có cần lọc cụm từ nào không. Đặc biệt, đừng xóa các từ phủ định như không, chưa nếu chúng ảnh hưởng đến ý nghĩa của văn bản.

## Character n-gram (là kỹ thuật chia một chuỗi văn bản thành các đoạn con liên tiếp dài đúng n ký tự)
```bash
Nó được dùng rất nhiều trong:
    - Phát hiện văn bản trùng lặp (duplicate detection)
    - MinHash
    - LSH (Locality Sensitive Hashing)
    - So sánh độ giống nhau của văn bản

Ý tưởng rất đơn giản:
    Trượt một cửa sổ dài 5 ký tự từ trái sang phải, mỗi lần dịch 1 ký tự.

Ví dụ 1
    Chuỗi: abcdefghi

    Character 5-gram sẽ là
        1. abcde
        2. bcdef
        3. cdefg
        4. defgh
        5. efghi
```
**Tại sao phải dùng n-gram?**
```bash
Nếu so sánh từng từ: hello world với hello word
    thì: world ≠ word -> mất hẳn sự tương đồng. -> Trong khi đó character 5-gram vẫn giữ được nhiều phần giống nhau.
```