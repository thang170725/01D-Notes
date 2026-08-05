
- [Text Proprocessing (tiền xử lý văn bản)](#text-proprocessing-tiền-xử-lý-văn-bản)
  - [Stopwords removal (loại bỏ từ không mang nhiều ý nghĩa)](#stopwords-removal-loại-bỏ-từ-không-mang-nhiều-ý-nghĩa)
  - [Punctuation (dấu câu)](#punctuation-dấu-câu)
  - [Stemming](#stemming)
  - [Lemmatization](#lemmatization)
  - [Unicode Normalization (chuẩn hóa bảng mã unicode)](#unicode-normalization-chuẩn-hóa-bảng-mã-unicode)
    - [NFC (Lưu thànhh 1 ký tự duy nhất)](#nfc-lưu-thànhh-1-ký-tự-duy-nhất)
    - [NFD (lưu thành các kí tự riêng)](#nfd-lưu-thành-các-kí-tự-riêng)
- [Tokenization](#tokenization)
  - [Word-level Tokenization (Cắt câu theo dấu cách hoặc dấu câu)](#word-level-tokenization-cắt-câu-theo-dấu-cách-hoặc-dấu-câu)
  - [Subword Tokenization](#subword-tokenization)
    - [BPE (Byte Pair Encoding)](#bpe-byte-pair-encoding)
    - [WordPiece](#wordpiece)
    - [Unigram Language Model (SentencePiece) (Chọn subword tối ưu bằng mô hình ngôn ngữ xác suất)](#unigram-language-model-sentencepiece-chọn-subword-tối-ưu-bằng-mô-hình-ngôn-ngữ-xác-suất)
    - [Byte-level BPE (Tokenize thẳng trên bytes → không phụ thuộc unicode)](#byte-level-bpe-tokenize-thẳng-trên-bytes--không-phụ-thuộc-unicode)
    - [Transformer embeddings](#transformer-embeddings)
      - [CRF (Character-level Tokenization)](#crf-character-level-tokenization)
      - [Post-Tokenization Processing](#post-tokenization-processing)
---
# Text Proprocessing (tiền xử lý văn bản)
```bash
Tiền xử lý — giảm kích thước bộ từ và tăng chất lượng feature cho TF/Count
```
## Stopwords removal (loại bỏ từ không mang nhiều ý nghĩa)
```bash
Ý tưởng: danh sách các từ “không mang nhiều ý nghĩa” như “và”, “là”, “the”, “a” — thường loại bỏ trước khi xử lý để giảm noise và kích thước feature.
    Lưu ý: với một số tác vụ (ví dụ sentiment, questions), stopwords có thể mang thông tin (ví dụ “not” cực kỳ quan trọng) → cẩn thận khi loại.
```
## Punctuation (dấu câu)
```bash
Vì sao phải xử lý punctuation?
    Ví dụ:
        hello
        hello!
        hello?

        Máy tính có thể coi đây là:
            "hello"
            "hello!"
            "hello?"
        => là 3 token khác nhau.
        
        Nên trong NLP truyền thống thường:
            hello!
            ↓
            hello
        => Loại bỏ: . , ! ? ; : ( ) [ ] { } " '
            Ví dụ:
                "Tôi thích AI!!!"
                    ↓
                toi thich ai
```
## Stemming
```bash
Ý tưởng: Cắt đuôi từ để đưa về dạng gốc thô bằng cách dùng rule cứng (heuristics). 
    - Không quan tâm ngữ pháp. 
    - Không đảm bảo trả về từ có nghĩa.
    - Cách làm: cắt suffix kiểu “ing”, “ed”, “ly”, “s”, …

Dùng để làm gì: 
    - giảm số lượng dạng của từ, 
    - đơn giản hoá văn bản để dùng cho TF-IDF, bag-of-words, search,…
```
## Lemmatization
```bash
Ý tưởng: đưa từ về dạng nguyên mẫu có nghĩa (lemma) dựa trên từ điển + phân tích ngữ pháp. 
    - Dùng mô hình ngôn ngữ / từ điển. Trả về từ hợp lệ của ngôn ngữ. Hiểu ngữ cảnh của từ trong câu.
    - xử lý NLP có yêu cầu ngữ nghĩa tốt hơn information extraction, question answering, machine translationToken

Là một đơn vị nhỏ mà mô hình NLP sử dụng để xử lý văn bản. Nó không nhất thiết phải là một từ:
    • Một từ: ví dụ "bật", "nhạc"
    • Một từ gốc: "chơi" từ "chơi nhạc"
    • Một tiếng (âm tiết): trong tiếng Việt rất phổ biến
    • Thậm chí là một nửa từ (vì mô hình học theo kiểu cắt nhỏ)
```
## Unicode Normalization (chuẩn hóa bảng mã unicode)
```bash
Máy tính không lưu chữ. Máy tính lưu số.
    Ví dụ:
        A -> 65
        B -> 66

Unicode là bảng quy định:
    á
    à
    ả
    ã
    ...
=> được biểu diễn thế nào.

Vấn đề với tiếng Việt
    Một chữ: ế
=> có thể được lưu theo 2 cách khác nhau.
```
**Thực tế Production Pipeline thường là**
```bash
Raw Text
   ↓
Unicode Normalize (NFC)
   ↓
Lowercase
   ↓
Remove Punctuation
   ↓
Tokenization

Ví dụ:
"TÔI THÍCH LẬP TRÌNH!!!"
↓
Unicode Normalize
↓
"TÔI THÍCH LẬP TRÌNH!!!"
↓
Lowercase
"tôi thích lập trình!!!"
↓
Remove punctuation
"tôi thích lập trình"
↓
Tokenize
["tôi", "thích", "lập", "trình"]
```
### NFC (Lưu thànhh 1 ký tự duy nhất)
### NFD (lưu thành các kí tự riêng)
**Ex: Ví dụ thực tế**
```bash
Bạn có database:
    Thế Giới Di Động

Người dùng nhập:
    Thế Giới Di Động
=> Nhìn giống hệt.

Nhưng: text1 == text2
    có thể: False, vì một bên là NFC, một bên là NFD.
```
# Tokenization 
## Word-level Tokenization (Cắt câu theo dấu cách hoặc dấu câu)
```bash
Dùng trong mô hình NLP cổ điển như Bag-of-Words, TF-IDF, Word2Vec, LSTM cũ,...

Nhược điểm:
    - Không xử lý được từ mới (OOV)
    - không phù hợp với ngôn ngữ biến hình (như tiếng Việt, tiếng Đức…).
```
## Subword Tokenization
```bash
Đây là phương pháp đứng sau các mô hình hiện đại như:
    - PhoBERT
    - BARTpho
    - XLM-R
    - mBERT
    - GPT
    - LLaMA
    - Qwen
    - v.v
=> sống khỏe trong mọi hệ thống NLP từ 2020 đến 2025
```
### BPE (Byte Pair Encoding)
```bash
Là một kỹ thuật tokenization hiện đại và phổ biến nhất dùng trong GPT-2, GPT-3, RoBERTa, XLM-R, PhoBERT. 
    Rộng rãi nhất trong các mô hình open-source → Học sâu
```
**Cách hoạt động**
```bash
bằng cách ghép các cặp ký tự/subword phổ biến nhất. 

BPE phải có </w>? 
    Vì BPE hoạt động bằng cách merge các cặp ký tự/token
    nếu không có end marker => BPE sẽ merge xuyên qua ranh giới giữa các từ → làm hỏng cấu trúc từ.
```
**Ex: workfollow của BPE**
```bash
Giả sử tập dữ liệu chỉ có:
    - low
    - lower
    - lowest
```
```bash
1. Ban đầu BPE tách thành từng ký tự:
    - l o w
    - l o w e r
    - l o w e s t

2. Đếm cặp ký tự xuất hiện nhiều nhất
    Các cặp:
        - l o
        - o w
        - w e
        - e r
        - e s
        - s t
    Giả sử:
        - l o  -> xuất hiện 3 lần
        - o w  -> xuất hiện 3 lần
    BPE chọn một cặp phổ biến nhất, ví dụ:
        l + o = lo
    
    Vocabulary mới:
        lo
        w
        e
        r
        s
        t
    Chuỗi trở thành:
        lo w
        lo w e r
        lo w e s t

3. Đếm lại:
    lo w -> 3 lần
    Gộp:
        lo + w = low
    Kết quả:
        low
        low e r
        low e s t

4. Đếm lại:
    low e -> 2 lần
    
    Gộp:
        lowe
    Kết quả:
    low
    lowe r
    lowe s t

Vocabulary cuối cùng Có thể là:
    l
    o
    w
    e
    r
    s
    t
    lo
    low
    lowe

Khi encode từ mới Ví dụ: lowest
    BPE sẽ cố tìm token dài nhất trong vocabulary:
        lowe + st hoặc low + est (tùy vocabulary đã học được)
```
### WordPiece
```bash
Phổ biến nhất trong BERT, RoBERTa, ALBERT, … → Biết cách dùng, không cần học sâu (ít mô hình mới dùng)

Là thuật toán tách từ thành các mảnh nhỏ (subword). Mục tiêu chính:
    - Giảm số lượng từ trong vocab, vì nhiều từ hiếm → khó học.
    - Xử lý từ mới (OOV - out of vocabulary): nếu mô hình chưa từng thấy từ đó, nó vẫn có thể hiểu nhờ các mảnh subword.
    - Giống BPE nhưng tối ưu bằng xác suất có điều kiện: BERT, mBERT, DistilBERT
```
**Ex**
```bash
Với câu "playing plays played"
    1. Bắt đầu: [p][l][a][y][i][n][g]
    2. Ghép thường xuyên: "pl", "play"
    3. Tiếp tục học "##ing", "##ed", "##s"
→ Cuối cùng vocab có thể gồm: ["[PAD]", "[UNK]", "play", "##ing", "##ed", "##s"]
```
**Ex2: sử dụng wordPiece với transformer**
```python
from transformers import BertTokenizer

# Dùng tokenizer của BERT (WordPiece)
tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")

sentence = "Playing football is amazing"
tokens = tokenizer.tokenize(sentence)
ids = tokenizer.convert_tokens_to_ids(tokens)

print("Tokens:", tokens)
print("IDs:", ids)
# Tokens: ['playing', 'football', 'is', 'amazing']
# IDs: [2652, 2374, 2003, 6429]

# Nếu bạn nhập từ mới lạ như "playfulness", BERT chưa từng thấy nguyên từ đó, nhưng WordPiece vẫn xử lý được
tokens = tokenizer.tokenize("playfulness")
print(tokens) # ['play', '##ful', '##ness']
```
### Unigram Language Model (SentencePiece) (Chọn subword tối ưu bằng mô hình ngôn ngữ xác suất)
```bash
Dùng trong T5, mT5, UL2, PaLM, Flan series. Mạnh cho đa ngôn ngữ. → Học khá sâu
```
### Byte-level BPE (Tokenize thẳng trên bytes → không phụ thuộc unicode)
```bash
Dùng trong GPT-2, GPT-3, GPT-4, LlaMA-3. → Hiểu khái niệm là đủ (rất giống BPE)

Biến thể của BPE ở cấp byte, xử lý tốt đa ngôn ngữ, emoji, ký tự lạ. GPT-2, GPT-3, GPT-4, LLaMA-2/3
```
### Transformer embeddings
```bash
Phù hợp khi cần mô hình hiểu ngữ cảnh phức tạp, dữ liệu đa dạng, ngôn ngữ tự nhiên đầy đủ, nhiều dữ liệu huấn luyện (ít nhất vài nghìn câu)
```
#### CRF (Character-level Tokenization)
```bash
Tách từng ký tự, không bao giờ OOV.

Nhược điểm: 
    - chuỗi rất dài
    - học chậm
    - mất ngữ nghĩa cao cấp.

Ứng dụng: các mô hình nghiên cứu ngôn ngữ đặc biệt (ví dụ xử lý lỗi chính tả, OCR, mã hóa DNA,…). 
    Dùng trong Char-CNN, Char-RNN, hoặc một số mô hình hybrid (kết hợp subword + char).
```
#### Post-Tokenization Processing