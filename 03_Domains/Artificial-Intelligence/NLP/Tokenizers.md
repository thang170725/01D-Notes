Token
Là một đơn vị nhỏ mà mô hình NLP sử dụng để xử lý văn bản. Nó không nhất thiết phải là một từ:
    • Một từ: ví dụ "bật", "nhạc"
    • Một từ gốc: "chơi" từ "chơi nhạc"
    • Một tiếng (âm tiết): trong tiếng Việt rất phổ biến
    • Thậm chí là một nửa từ (vì mô hình học theo kiểu cắt nhỏ)
Cú pháp:
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")
sentence = "bật nhạc lofi chill"
tokens = tokenizer.tokenize(sentence)

print(tokens) # ['bật', 'nhạc', 'lo', '##fi', 'chill']Word-level Tokenization
    • Cắt câu theo dấu cách hoặc dấu câu. Không xử lý được từ mới (OOV), không phù hợp với ngôn ngữ biến hình (như tiếng Việt, tiếng Đức…).
    • Dùng trong mô hình NLP cổ điển như Bag-of-Words, TF-IDF, Word2Vec, LSTM cũ,...
Subword Tokenization
Đây là phương pháp đứng sau các mô hình hiện đại như. PhoBERT, BARTpho, XLM-R, mBERT, GPT, LLaMA, Qwen, v.v. VÀ sống khỏe trong mọi hệ thống NLP từ 2020 đến 2025. Nếu bạn học sâu 1 thứ → hãy học cái này.
BPE (Byte Pair Encoding)
    • Là một kỹ thuật tokenization hiện đại và phổ biến nhất dùng trong GPT-2, GPT-3, RoBERTa, XLM-R, PhoBERT. Rộng rãi nhất trong các mô hình open-source → Học sâu
    • bằng cách ghép các cặp ký tự/subword phổ biến nhất. 
    • BPE phải có </w>? Vì BPE hoạt động bằng cách merge các cặp ký tự/token, và nếu không có end marker, BPE sẽ merge xuyên qua ranh giới giữa các từ → làm hỏng cấu trúc từ.
Bài tập
BPE thực chất là tổng hợp của các bài toán nhỏ hơn. Thông qua các bài tập nhỏ này có thể ghép lại và code được BPE
Tách chuỗi "hello" thành ["h", "e", "l", "l", "o"]
def split(text: str):
    return [t for t in text]
Nối các phần tử của mảng ["he", "l", "lo"] thành "he l lo"
def split(li: list):
    return ' '.join(li)

print(split(["he", "l", "lo"])) # he l lo
Tách chữ thành ký tự và đếm tần suất mỗi ký tự
def counts(lines: list):
    # 1. Tách ký tự và gộp thành 1 list
    chars = []
    for line in lines:
        for ch in line:
            if ch != " ":       # bỏ khoảng trắng
                chars.append(ch)
    
    # 2. Đếm tần suất
    freq = {}
    for ch in chars:
        freq[ch] = freq.get(ch, 0) + 1

    return freq

print(counts(["hello world", "hello"]))
Tạo danh sách tất cả các cặp ký tự liền nhau
def bigrams_from_string(s: str):
    return [(s[i], s[i+1]) for i in range(len(s)-1)]

print(bigrams_from_string("hello")) # [('h','e'), ('e','l'), ('l','l'), ('l','o')]
Tìm bigram xuất hiện nhiều nhất
def most_bigram_frequency(big: list):
    # big: list of tuple
    freq = {}
    for b in big:
        freq[b] = freq.get(b, 0) + 1

    best_count = -1
    best_bigram = None
    for k, v in freq.items():
        if v > best_count:
            best_count = v
            best_bigram = k

    return freq, (best_bigram, best_count)

input_data = [("h","e"), ("e","l"), ("l","l"), ("l","o")]
print(most_bigram_frequency(input_data))
# Expected: ({('h','e'):1, ('e','l'):1, ('l','l'):1, ('l','o'):1}, (('h','e'),1))
# Note: all have count 1 so first-seen is returned as "best"
from collections import Counter

def most_bigram_frequency(big: list):
    cnt = Counter(big)
    if not cnt:
        return {}, (None, 0)
    most_common_bigram, freq = cnt.most_common(1)[0]
    return dict(cnt), (most_common_bigram, freq)

input_data = [("h","e"), ("e","l"), ("l","l"), ("l","o")]
print(most_bigram_frequency(input_data))
from collections import Counter

def most_bigram_frequency(big: list):
    cnt = Counter(big)
    if not cnt:
        return {}, (None, 0)
    most_common_bigram, freq = cnt.most_common(1)[0]
    return dict(cnt), (most_common_bigram, freq)

input_data = [("h","e"), ("e","l"), ("l","l"), ("l","o")]
print(most_bigram_frequency(input_data))
Replace một bigram trong danh sách token
def replace_pair(tokens_list, pair, new_token):
    out = []
    for tokens in tokens_list:
        merged = []
        i = 0
        while i < len(tokens):
            if i < len(tokens)-1 and (tokens[i], tokens[i+1]) == pair:
                merged.append(new_token)
                i += 2
            else:
                merged.append(tokens[i])
                i += 1
        out.append(merged)
    return out

WordPiece
    • Phổ biến nhất trong BERT, RoBERTa, ALBERT, … → Biết cách dùng, không cần học sâu (ít mô hình mới dùng)
    • Là thuật toán tách từ thành các mảnh nhỏ (subword). Mục tiêu chính:
        ◦ Giảm số lượng từ trong vocab, vì nhiều từ hiếm → khó học.
        ◦ Xử lý từ mới (OOV - out of vocabulary): nếu mô hình chưa từng thấy từ đó, nó vẫn có thể hiểu nhờ các mảnh subword.
    • Giống BPE nhưng tối ưu bằng xác suất có điều kiện: BERT, mBERT, DistilBERT
Ví dụ:
Với câu "playing plays played"
    1. Bắt đầu: [p][l][a][y][i][n][g]
    2. Ghép thường xuyên: "pl", "play"
    3. Tiếp tục học "##ing", "##ed", "##s"
→ Cuối cùng vocab có thể gồm: ["[PAD]", "[UNK]", "play", "##ing", "##ed", "##s"]
Cú pháp:
from transformers import BertTokenizer

# Dùng tokenizer của BERT (WordPiece)
tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")

sentence = "Playing football is amazing"
tokens = tokenizer.tokenize(sentence)
ids = tokenizer.convert_tokens_to_ids(tokens)

print("Tokens:", tokens)
print("IDs:", ids)
Tokens: ['playing', 'football', 'is', 'amazing']
IDs: [2652, 2374, 2003, 6429]
# Nếu bạn nhập từ mới lạ như "playfulness", BERT chưa từng thấy nguyên từ đó, nhưng WordPiece vẫn xử lý được

tokens = tokenizer.tokenize("playfulness")
print(tokens)
['play', '##ful', '##ness']
Unigram Language Model (SentencePiece)
    • Dùng trong T5, mT5, UL2, PaLM, Flan series. Mạnh cho đa ngôn ngữ. → Học khá sâu
    • Chọn subword tối ưu bằng mô hình ngôn ngữ xác suất.
Byte-level BPE
    • Tokenize thẳng trên bytes → không phụ thuộc unicode. Dùng trong GPT-2, GPT-3, GPT-4, LlaMA-3. → Hiểu khái niệm là đủ (rất giống BPE)
    • Biến thể của BPE ở cấp byte, xử lý tốt đa ngôn ngữ, emoji, ký tự lạ. GPT-2, GPT-3, GPT-4, LLaMA-2/3
Transformer embeddings
Phù hợp khi cần mô hình hiểu ngữ cảnh phức tạp, dữ liệu đa dạng, ngôn ngữ tự nhiên đầy đủ, nhiều dữ liệu huấn luyện (ít nhất vài nghìn câu)
CRF
Character-level Tokenization
    • Tách từng ký tự, không bao giờ OOV.
    • Nhược điểm: chuỗi rất dài, học chậm, mất ngữ nghĩa cao cấp.
    • Ứng dụng: các mô hình nghiên cứu ngôn ngữ đặc biệt (ví dụ xử lý lỗi chính tả, OCR, mã hóa DNA,…). Dùng trong Char-CNN, Char-RNN, hoặc một số mô hình hybrid (kết hợp subword + char).
Post-Tokenization Processing