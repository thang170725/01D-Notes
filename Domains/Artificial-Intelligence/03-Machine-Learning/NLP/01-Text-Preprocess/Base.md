
Stopwords removal
    • Ý tưởng: danh sách các từ “không mang nhiều ý nghĩa” như “và”, “là”, “the”, “a” — thường loại bỏ trước khi xử lý để giảm noise và kích thước feature.
    • Tiền xử lý — giảm kích thước bộ từ và tăng chất lượng feature cho TF/Count.
    • Lưu ý: với một số tác vụ (ví dụ sentiment, questions), stopwords có thể mang thông tin (ví dụ “not” cực kỳ quan trọng) → cẩn thận khi loại.
Stemming
    • Ý tưởng: Cắt đuôi từ để đưa về dạng gốc thô bằng cách dùng rule cứng (heuristics). Không quan tâm ngữ pháp. Không đảm bảo trả về từ có nghĩa.
    • Cách làm: cắt suffix kiểu “ing”, “ed”, “ly”, “s”, …
    • Dùng để làm gì: giảm số lượng dạng của từ, đơn giản hoá văn bản để dùng cho TF-IDF, bag-of-words, search,…
Lemmatization
    • Ý tưởng: đưa từ về dạng nguyên mẫu có nghĩa (lemma) dựa trên từ điển + phân tích ngữ pháp. Dùng mô hình ngôn ngữ / từ điển. Trả về từ hợp lệ của ngôn ngữ. Hiểu ngữ cảnh của từ trong câu.
    • xử lý NLP có yêu cầu ngữ nghĩa tốt hơn information extraction, question answering, machine translationToken
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
# BPE (Byte Pair Encoding)
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
from collections import Counter
from typing import List, Tuple, Dict

class BPESimple:
    def __init__(self, series: List[str], end_marker='</w>'):
        self.raw_series = series[:]                   # danh sách từ bản gốc
        self.end_marker = end_marker

        self.words_list = self._extract_words(series) # danh sách cách word từ corpus
        
        self.tokenized_words = [self._extract_words(w) for w in self.words_list]

        # biến lưu lịch sử merge
        self.merges: List[Tuple[Tuple[str, str], str]] = []

        # cập nhật khi train
        self.vocab = set(tok for tw in self.tokenized_words for tok in tw)
    
    # ---------------------------
    # 1) Tiền xử lý / helper
    # ---------------------------
    def _extract_words(self, series: List[str]) -> List[str]:
        '''
        tách word bằng whitespace -> trả về list các word
        '''
        words = []
        for s in series:
            for w in s.split():
                words.append(w)
        return words

    
    def _word_to_tokens(self, word: str) -> List[str]:
        '''
        biểu diễn 1 word dưới dạng list ký tự + end_marker
        ví dụ: "hello" -> ['h', 'e', 'l', 'l', 'o', '</w>']
        '''
        return [ch for ch in word] + [self.end_marker]


    # ---------------------------------
    # 2) Tạo bigrams & đếm tần suất
    # ---------------------------------
    def _bigrams_from_token_list(self, tokens: List[str]) -> List[Tuple[str, str]]:
        '''
        Từ 1 token list trả về danh sách bigram (liền kề, overlapping)
        ví dụ: ['h', 'e', 'l', 'l', 'o', '</w>'] 
        -> [('h','e'), ('e','l'), ('l','l'), ('l','o'), ('o','</w>')]
        '''
        return [(tokens[i], tokens[i+1]) for i in range(len(tokens)-1)]
    
    def get_all_bigrams_counts(self) -> Counter:
        '''
        Tính tần suất của tất cả bigram trên toàn bộ tokenized_words.
        Trả về Counter mapping (bigram_tuple -> count).
        '''
        cnt = Counter()
        for tokens in self.tokenized_words:
            for bg in self._bigrams_from_token_list(tokens):
                cnt[bg] += 1
        return cnt
    
    # ---------------------------------
    # 3) Tìm bigram phổ biến nhất
    # ---------------------------------
    def most_frequent_bigram(self):
        """
        Trả về (best_bigram_tuple, frequency).
        Nếu không có bigram (corpus rỗng) trả về (None, 0)
        """
        cnt = self.get_all_bigrams_counts()
        if not cnt:
            return None, 0
        bigram, freq = cnt.most_common(1)[0]
        return bigram, freq

    # ---------------------------
    # 4) Replace/merge pair trong toàn bộ tokenized_words (1 step)
    # ---------------------------
    def replace_pair(self, pair: Tuple[str,str], new_token: str):
        """
        Thay thế tất cả occurrences của pair (a,b) bằng new_token trên toàn corpus (self.tokenized_words).
        Thao tác in-place (cập nhật self.tokenized_words).
        Logic:
            - duyệt từng word (tokens list)
            - duyệt token theo index i; nếu tokens[i], tokens[i+1] == pair -> append new_token và i += 2
              else: append tokens[i] và i += 1
        """
        new_tokenized = []
        for tokens in self.tokenized_words:
            merged = []
            i = 0
            while i < len(tokens):
                if i < len(tokens) - 1 and (tokens[i], tokens[i+1]) == pair:
                    # merge pair -> new token
                    merged.append(new_token)
                    i += 2  # skip next because đã merge
                else:
                    merged.append(tokens[i])
                    i += 1
            new_tokenized.append(merged)

        # cập nhật tokenized words và vocab
        self.tokenized_words = new_tokenized
        # cập nhật vocab: thêm new_token
        self.vocab.add(new_token)
    
from collections import Counter
from typing import List, Tuple, Dict

class BPESimple:
    """
    Một implementation BPE rất đơn giản, phù hợp để học/giải thích.
    - Huấn luyện (train) bằng num_merges bước merge.
    - Tokenization nội bộ: xử lý theo từng 'word' (mỗi 'word' là một unit, ví dụ tiếng/cụm không chứa space).
    - Dùng end-of-word marker '</w>' để BPE không merge qua ranh giới từ.
    """

    def __init__(self, series: List[str], end_marker: str = '</w>'):
        """
        series: list các câu hoặc 'words' bạn muốn train trên đó.
                Ở ví dụ đơn giản này mình coi mỗi element là một câu -> tách thành words bằng split().
        end_marker: token dùng để đánh dấu kết thúc 1 từ (giúp BPE không merge qua khoảng trắng)
        """
        self.raw_series = series[:]           # giữ bản gốc để tham khảo
        self.end_marker = end_marker
        # words_list: danh sách các 'word' (chuỗi không chứa whitespace) từ corpus
        self.words_list = self._extract_words(series)
        # tokenized_words: list of list, mỗi phần tử là word biểu diễn bằng ký tự + end_marker
        self.tokenized_words = [self._word_to_tokens(w) for w in self.words_list]

        # merges: danh sách các rule đã merge theo thứ tự [(pair, new_token), ...]
        self.merges: List[Tuple[Tuple[str,str], str]] = []
        # vocab: set các token hiện có (cập nhật khi train), khởi tạo từ ký tự đơn + end_marker
        self.vocab = set(tok for tw in self.tokenized_words for tok in tw)

    # ---------------------------
    # 1) Tiền xử lý / helper
    # ---------------------------
    def _extract_words(self, series: List[str]) -> List[str]:
        """
        Tách các câu thành các 'word' đơn giản (split bằng whitespace).
        Trả về list các word.
        """
        words = []
        for s in series:
            # split mặc định theo whitespace -> trả về các tiếng / từ
            for w in s.split():
                words.append(w)
        return words

    def _word_to_tokens(self, word: str) -> List[str]:
        """
        Biểu diễn 1 word dưới dạng list ký tự + end_marker.
        Ví dụ: "hello" -> ['h','e','l','l','o','</w>']
        """
        return [ch for ch in word] + [self.end_marker]

    # ---------------------------
    # 2) Tạo bigrams & đếm tần suất
    # ---------------------------
    def _bigrams_from_token_list(self, tokens: List[str]) -> List[Tuple[str,str]]:
        """
        Từ 1 token list trả về danh sách bigram (liền kề, overlapping).
        Ví dụ ['h','e','l','l','o','</w>'] -> [('h','e'), ('e','l'), ('l','l'), ('l','o'), ('o','</w>')]
        """
        return [(tokens[i], tokens[i+1]) for i in range(len(tokens)-1)]

    def get_all_bigrams_counts(self) -> Counter:
        """
        Tính tần suất của tất cả bigram trên toàn bộ tokenized_words.
        Trả về Counter mapping (bigram_tuple -> count).
        """
        cnt = Counter()
        for tokens in self.tokenized_words:
            for bg in self._bigrams_from_token_list(tokens):
                cnt[bg] += 1
        return cnt

    # ---------------------------
    # 3) Tìm bigram phổ biến nhất
    # ---------------------------
    def most_frequent_bigram(self) -> Tuple[Tuple[str,str], int]:
        """
        Trả về (best_bigram_tuple, frequency).
        Nếu không có bigram (corpus rỗng) trả về (None, 0)
        """
        cnt = self.get_all_bigrams_counts()
        if not cnt:
            return None, 0
        bigram, freq = cnt.most_common(1)[0]
        return bigram, freq

    # ---------------------------
    # 4) Replace/merge pair trong toàn bộ tokenized_words (1 step)
    # ---------------------------
    def replace_pair(self, pair: Tuple[str,str], new_token: str):
        """
        Thay thế tất cả occurrences của pair (a,b) bằng new_token trên toàn corpus (self.tokenized_words).
        Thao tác in-place (cập nhật self.tokenized_words).
        Logic:
            - duyệt từng word (tokens list)
            - duyệt token theo index i; nếu tokens[i], tokens[i+1] == pair -> append new_token và i += 2
              else: append tokens[i] và i += 1
        """
        new_tokenized = []
        for tokens in self.tokenized_words:
            merged = []
            i = 0
            while i < len(tokens):
                if i < len(tokens) - 1 and (tokens[i], tokens[i+1]) == pair:
                    # merge pair -> new token
                    merged.append(new_token)
                    i += 2  # skip next because đã merge
                else:
                    merged.append(tokens[i])
                    i += 1
            new_tokenized.append(merged)

        # cập nhật tokenized words và vocab
        self.tokenized_words = new_tokenized
        # cập nhật vocab: thêm new_token
        self.vocab.add(new_token)

    # ---------------------------
    # 5) Huấn luyện BPE: lặp merge N lần
    # ---------------------------
    def train(self, num_merges: int = 10, verbose: bool = True):
        """
        Thực hiện num_merges bước merge.
        Mỗi bước:
            1) tính tần suất bigram
            2) chọn bigram phổ biến nhất
            3) tạo token mới = concat 2 token cũ (ví dụ 'l'+'l' -> 'll')
            4) replace_pair trên toàn corpus
            5) lưu merge rule vào self.merges
        """
        for step in range(num_merges):
            bigram, freq = self.most_frequent_bigram()
            if bigram is None or freq == 0:
                if verbose:
                    print(f"[step {step}] No more bigrams to merge.")
                break

            # tạo tên token mới (ghép hai token cũ). Bạn có thể dùng một separator nếu muốn.
            new_token = ''.join(bigram)  # ví dụ ('l','l') -> 'll'
            # tránh trùng token mới nếu đã tồn tại; nếu trùng thì thêm suffix số (rất hiếm)
            if new_token in self.vocab:
                suffix = 1
                while f"{new_token}_{suffix}" in self.vocab:
                    suffix += 1
                new_token = f"{new_token}_{suffix}"

            # ghi nhận và replace
            if verbose:
                print(f"[step {step}] Merging {bigram} (freq={freq}) -> '{new_token}'")
            self.replace_pair(bigram, new_token)
            self.merges.append((bigram, new_token))

    # ---------------------------
    # 6) Encode: dùng merges đã học để tokenize text mới
    # ---------------------------
    def encode_word(self, word: str) -> List[str]:
        """
        Tokenize 1 word dùng rules đã học (self.merges).
        Cách làm đơn giản:
          - khởi tạo token list = [char,..., '</w>']
          - áp dụng các merge rules theo thứ tự đã học (lần lượt, mỗi rule merge tất cả occurrences trong word)
        Trả về list token (subwords)
        """
        tokens = self._word_to_tokens(word)
        for pair, new_token in self.merges:
            # apply replace step cho 1 word
            merged = []
            i = 0
            while i < len(tokens):
                if i < len(tokens)-1 and (tokens[i], tokens[i+1]) == pair:
                    merged.append(new_token)
                    i += 2
                else:
                    merged.append(tokens[i])
                    i += 1
            tokens = merged
        return tokens

    def encode(self, text: str) -> List[List[str]]:
        """
        Tokenize 1 câu/chuỗi text:
          - split thành words
          - encode từng word bằng encode_word
        Trả về danh sách các token lists tương ứng với các word.
        """
        out = []
        for w in text.split():
            out.append(self.encode_word(w))
        return out

    # ---------------------------
    # 7) Utility: get vocab / merges
    # ---------------------------
    def get_merges(self) -> List[Tuple[Tuple[str,str], str]]:
        """Trả về danh sách merges đã học."""
        return self.merges[:]

    def get_vocab(self) -> set:
        """Trả về tập vocab hiện tại (các token xuất hiện trong tokenized_words)."""
        vocab = set(tok for tw in self.tokenized_words for tok in tw)
        return vocab

# ---------------------------
# Example chạy thử
# ---------------------------
if __name__ == "__main__":
    series = [
        "xin chào tôi tên là thắng",
        "bạn có khỏe không",
        "xin chào bạn",
        "tôi khỏe"
    ]

    # Khởi tạo
    bpe = BPESimple(series)

    print("=== Words extracted from corpus ===")
    print(bpe.words_list)
    print()

    print("=== Initial tokenized words (char level + </w>) ===")
    for tw in bpe.tokenized_words:
        print(tw)
    print()

    # Train với 10 merges (bạn có thể thay đổi)
    bpe.train(num_merges=10, verbose=True)
    print()

    print("=== Merges learned (in order) ===")
    for m in bpe.get_merges():
        print(m)
    print()

    print("=== Tokenized corpus after merges ===")
    for tw in bpe.tokenized_words:
        print(tw)
    print()

    print("=== Vocab (sample) ===")
    print(sorted(list(bpe.get_vocab()))[:50])
    print()

    # Encode 1 câu mới
    text = "xin chào"
    print(f"Encoding '{text}' ->")
    print(bpe.encode(text))
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