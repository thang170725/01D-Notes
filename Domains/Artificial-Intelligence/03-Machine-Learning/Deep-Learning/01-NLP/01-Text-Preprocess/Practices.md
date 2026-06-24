- [BPE (Byte-Pair Encoding)](#bpe-byte-pair-encoding)
  - [Tách chuỗi "hello" thành \["h", "e", "l", "l", "o"\]](#tách-chuỗi-hello-thành-h-e-l-l-o)
  - [Nối các phần tử của mảng \["he", "l", "lo"\] thành "he l lo"](#nối-các-phần-tử-của-mảng-he-l-lo-thành-he-l-lo)
  - [Tách chữ thành ký tự và đếm tần suất mỗi ký tự](#tách-chữ-thành-ký-tự-và-đếm-tần-suất-mỗi-ký-tự)
  - [Tạo danh sách tất cả các cặp ký tự liền nhau](#tạo-danh-sách-tất-cả-các-cặp-ký-tự-liền-nhau)
  - [Tìm bigram xuất hiện nhiều nhất](#tìm-bigram-xuất-hiện-nhiều-nhất)
  - [Replace một bigram trong danh sách token](#replace-một-bigram-trong-danh-sách-token)
  - [Demo BPE](#demo-bpe)
---
# BPE (Byte-Pair Encoding)
```bash
BPE thực chất là tổng hợp của các bài toán nhỏ hơn. Thông qua các bài tập nhỏ này có thể ghép lại và code được BPE
```
## Tách chuỗi "hello" thành ["h", "e", "l", "l", "o"]
```python
def split(text: str):
    return [t for t in text]
```
## Nối các phần tử của mảng ["he", "l", "lo"] thành "he l lo"
```python
def split(li: list):
    return ' '.join(li)

print(split(["he", "l", "lo"])) # he l lo
```
## Tách chữ thành ký tự và đếm tần suất mỗi ký tự
```python
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
```
## Tạo danh sách tất cả các cặp ký tự liền nhau
```python
def bigrams_from_string(s: str):
    return [(s[i], s[i+1]) for i in range(len(s)-1)]

print(bigrams_from_string("hello")) # [('h','e'), ('e','l'), ('l','l'), ('l','o')]
```
## Tìm bigram xuất hiện nhiều nhất
```python
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
```
## Replace một bigram trong danh sách token
```python
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
```
## Demo BPE
```python
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
```
```python 
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
```