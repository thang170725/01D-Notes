- [BPE (Byte-Pair Encoding)](#bpe-byte-pair-encoding)
  - [Tách chuỗi "hello" thành \["h", "e", "l", "l", "o"\]](#tách-chuỗi-hello-thành-h-e-l-l-o)
  - [Nối các phần tử của mảng \["he", "l", "lo"\] thành "he l lo"](#nối-các-phần-tử-của-mảng-he-l-lo-thành-he-l-lo)
  - [Tách chữ thành ký tự và đếm tần suất mỗi ký tự](#tách-chữ-thành-ký-tự-và-đếm-tần-suất-mỗi-ký-tự)
  - [Tạo danh sách tất cả các cặp ký tự liền nhau](#tạo-danh-sách-tất-cả-các-cặp-ký-tự-liền-nhau)
  - [Tìm bigram xuất hiện nhiều nhất](#tìm-bigram-xuất-hiện-nhiều-nhất)
  - [Replace một bigram trong danh sách token](#replace-một-bigram-trong-danh-sách-token)
  - [Demo full pipeline BPE](#demo-full-pipeline-bpe)
---
# Demo pipeline thuật toán BPE code thuần
```python
from collections import Counter
from typing import List, Tuple, Dict, Set

class BPESimple:
    """
    A very simple Byte Pair Encoding (BPE) implementation for educational purposes.
    - Trains using a specified number of merge steps.
    - Internal tokenization operates at the word level (whitespace-separated units).
    - Uses an end-of-word marker '</w>' to prevent merging across word boundaries.
    """

    def __init__(self, series: List[str], end_marker: str = '</w>'):
        self.end_marker = end_marker
        self.series = series
        
        # Internal states managed during pipeline and training
        self.merges: List[Tuple[Tuple[str, str], str]] = []
        self.tokenized_words: List[List[str]] = []
        self.vocab: Set[str] = set()

    # 1. Extract words from corpus
    def _extract_words(self, series: List[str]) -> List[str]:
        """
        Split sentences into a list of words by whitespace.
        Example: ["hello world"] -> ['hello', 'world']
        """
        words = []
        for s in series:
            for w in s.split():
                words.append(w)
        
        print("\n--- [Step 1: Extract Words] ---")
        print("Words extracted from corpus:\n", words)
        return words

    # 2. Convert words to initial characters + end marker
    def _word_to_tokens(self, word_list: List[str]) -> List[List[str]]:
        """
        Example: ["hello", "i"] -> [['h','e','l','l','o','</w>'], ['i', '</w>']]
        """
        tokenized = []
        for word in word_list:
            tokenized.append([ch for ch in word] + [self.end_marker])
        
        print("\n--- [Step 2: Initialize Tokens] ---")
        print("Initial tokenized words (char level + </w>):\n", tokenized)
        return tokenized

    # 3. Create bigrams from token list
    def _bigrams_from_token_list(self, tokenized_words: List[List[str]]) -> List[Tuple[str, str]]:
        """
        Extract adjacent, overlapping bigrams from token lists.
        Example: [['h','e','l']] -> [('h','e'), ('e','l')]
        """
        all_bigrams = []
        for tokens in tokenized_words:
            for i in range(len(tokens) - 1):
                all_bigrams.append((tokens[i], tokens[i+1]))

        print("\n--- [Step 3: Extract Bigrams] ---")
        print("Bigrams extracted from current token list (showing first 15):\n", all_bigrams[:15])
        return all_bigrams
   
    # 4. Count bigram frequencies
    def _get_all_bigrams_counts(self, bigrams_from_token_list: List[Tuple[str, str]]) -> Counter:
        cnt = Counter(bigrams_from_token_list)
        print("\n--- [Step 4: Count Bigrams] ---")
        print("Top 5 bigram counts:\n", cnt.most_common(5))
        return cnt

    # 5. Find the most frequent bigram
    def most_frequent_bigram(self, bigrams_counts: Counter) -> Tuple[Tuple[str, str], int]:
        """
        Returns (best_bigram_tuple, frequency). Returns (None, 0) if empty.
        """     
        if not bigrams_counts:
            return None, 0
        bigram, freq = bigrams_counts.most_common(1)[0]
        print("\n--- [Step 5: Find Most Frequent Bigram] ---")
        print("Most frequent bigram:\n", (bigram, freq))
        return bigram, freq

    # 6. Merge the chosen pair across the entire corpus
    def replace_pair(self, pair: Tuple[str, str], new_token: str):
        """
        Example: ('x', 'i') -> "xi" in all tokenized words
        """
        new_tokenized = []
        for tokens in self.tokenized_words:
            merged = []
            i = 0
            while i < len(tokens):
                if i < len(tokens) - 1 and (tokens[i], tokens[i+1]) == pair:
                    merged.append(new_token)  # Merge pair into new token
                    i += 2                    # Skip next token since it's merged
                else:
                    merged.append(tokens[i])
                    i += 1
            new_tokenized.append(merged)

        # Update the state of the corpus and vocabulary
        self.tokenized_words = new_tokenized
        self.vocab.add(new_token)

    # 7. Train BPE model
    def train(self, num_merges: int, verbose: bool = True):
        """
        Perform a number of merge steps to learn subwords.
        """
        print(f"\n================ STARTING BPE TRAINING ({num_merges} merges) ================")
        
        # Initialize initial vocabulary set from current state
        self.vocab = set(tok for tw in self.tokenized_words for tok in tw)

        for step in range(num_merges):
            # Recalculate frequencies at each iteration based on current state
            bigrams = self._bigrams_from_token_list(self.tokenized_words)
            counts = self._get_all_bigrams_counts(bigrams)
            bigram, freq = self.most_frequent_bigram(counts)
            
            if bigram is None or freq == 0:
                if verbose:
                    print(f"[Step {step}] No more bigrams to merge.")
                break

            # Create a new token by combining the pair
            new_token = ''.join(bigram)
            
            # Prevent duplicate tokens if they already exist in the vocabulary
            if new_token in self.vocab:
                suffix = 1
                while f"{new_token}_{suffix}" in self.vocab:
                    suffix += 1
                new_token = f"{new_token}_{suffix}"

            if verbose:
                print(f"**[Step {step}] Merging pair {bigram} (freq={freq}) -> '{new_token}'**")
            
            # Apply merge rule to corpus and record it
            self.replace_pair(bigram, new_token)
            self.merges.append((bigram, new_token))

    # ---------------------------
    # Inference: Tokenize new text using learned merge rules
    # ---------------------------
    def encode_word(self, word: str) -> List[str]:
        """
        Tokenize a single word using learned merge rules (self.merges).
        """
        # Convert word to initial characters + end marker
        tokens = [ch for ch in word] + [self.end_marker]
        
        for pair, new_token in self.merges:
            merged = []
            i = 0
            while i < len(tokens):
                if i < len(tokens) - 1 and (tokens[i], tokens[i+1]) == pair:
                    merged.append(new_token)
                    i += 2
                else:
                    merged.append(tokens[i])
                    i += 1
            tokens = merged
        return tokens

    def encode(self, text: str) -> List[List[str]]:
        """
        Tokenize a full string/sentence by breaking it down into words.
        """
        out = []
        for w in text.split():
            out.append(self.encode_word(w))
        return out
    
    # ---------------------------
    # Utilities
    # ---------------------------
    def get_merges(self) -> List[Tuple[Tuple[str, str], str]]:
        return self.merges[:]

    def get_vocab(self) -> set:
        self.vocab = set(tok for tw in self.tokenized_words for tok in tw)
        return self.vocab
    
    def run_pipeline(self):
        print("================ STARTING PIPELINE INITIALIZATION ================")
        # 1. Extract words list from corpus
        words_list = self._extract_words(self.series)

        # 2. Tokenize words into list of characters + end_marker
        self.tokenized_words = self._word_to_tokens(words_list)

        # 3. Get bigrams from the initial token list
        bigrams_from_token_list = self._bigrams_from_token_list(self.tokenized_words)

        # 4. Get bigram counts
        bigrams_count = self._get_all_bigrams_counts(bigrams_from_token_list)

        # 5. Extract the most popular bigram
        bigram, freq = self.most_frequent_bigram(bigrams_count)
        print("================ PIPELINE INITIALIZATION COMPLETED ================\n")


# ===================
# ==== TESTING ======
# ===================
if __name__ == "__main__":
    # 1. Initialize data demo
    series: List[str] = [
        "xin chào tôi tên là thắng",
        "bạn có khỏe không",
        "xin chào bạn",
        "tôi khỏe"
    ]

    # 1.2 Create BPE instance
    bpe = BPESimple(series)

    # 2. Run pipeline to view processing flow
    bpe.run_pipeline()

    # 3. Train with 10 merges
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

    print("=== Vocab (Sample) ===")
    print(sorted(list(bpe.get_vocab())))
    print()

    # 4. Encode new text using learned vocabulary rules
    text = "xin chào thắng"
    print(f"Encoding text: '{text}' ->")
    print(bpe.encode(text))
```
**Result**
```bash
================ STARTING PIPELINE INITIALIZATION ================

--- [Step 1: Extract Words] ---
Words extracted from corpus:
 ['xin', 'chào', 'tôi', 'tên', 'là', 'thắng', 'bạn', 'có', 'khỏe', 'không', 'xin', 'chào', 'bạn', 'tôi', 'khỏe']

--- [Step 2: Initialize Tokens] ---
Initial tokenized words (char level + </w>):
 [['x', 'i', 'n', '</w>'], ['c', 'h', 'à', 'o', '</w>'], ['t', 'ô', 'i', '</w>'], ['t', 'ê', 'n', '</w>'], ['l', 'à', '</w>'], ['t', 'h', 'ắ', 'n', 'g', '</w>'], ['b', 'ạ', 'n', '</w>'], ['c', 'ó', '</w>'], ['k', 'h', 'ỏ', 'e', '</w>'], ['k', 'h', 'ô', 'n', 'g', '</w>'], ['x', 'i', 'n', '</w>'], ['c', 'h', 'à', 'o', '</w>'], ['b', 'ạ', 'n', '</w>'], ['t', 'ô', 'i', '</w>'], ['k', 'h', 'ỏ', 'e', '</w>']]

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('x', 'i'), ('i', 'n'), ('n', '</w>'), ('c', 'h'), ('h', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n'), ('n', '</w>'), ('l', 'à'), ('à', '</w>')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('n', '</w>'), 5), (('k', 'h'), 3), (('x', 'i'), 2), (('i', 'n'), 2), (('c', 'h'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('n', '</w>'), 5)
================ PIPELINE INITIALIZATION COMPLETED ================


================ STARTING BPE TRAINING (10 merges) ================

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('x', 'i'), ('i', 'n'), ('n', '</w>'), ('c', 'h'), ('h', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n'), ('n', '</w>'), ('l', 'à'), ('à', '</w>')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('n', '</w>'), 5), (('k', 'h'), 3), (('x', 'i'), 2), (('i', 'n'), 2), (('c', 'h'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('n', '</w>'), 5)
**[Step 0] Merging pair ('n', '</w>') (freq=5) -> 'n</w>'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('x', 'i'), ('i', 'n</w>'), ('c', 'h'), ('h', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('k', 'h'), 3), (('x', 'i'), 2), (('i', 'n</w>'), 2), (('c', 'h'), 2), (('h', 'à'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('k', 'h'), 3)
**[Step 1] Merging pair ('k', 'h') (freq=3) -> 'kh'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('x', 'i'), ('i', 'n</w>'), ('c', 'h'), ('h', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('x', 'i'), 2), (('i', 'n</w>'), 2), (('c', 'h'), 2), (('h', 'à'), 2), (('à', 'o'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('x', 'i'), 2)
**[Step 2] Merging pair ('x', 'i') (freq=2) -> 'xi'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('xi', 'n</w>'), ('c', 'h'), ('h', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('xi', 'n</w>'), 2), (('c', 'h'), 2), (('h', 'à'), 2), (('à', 'o'), 2), (('o', '</w>'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('xi', 'n</w>'), 2)
**[Step 3] Merging pair ('xi', 'n</w>') (freq=2) -> 'xin</w>'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('c', 'h'), ('h', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n'), ('n', 'g')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('c', 'h'), 2), (('h', 'à'), 2), (('à', 'o'), 2), (('o', '</w>'), 2), (('t', 'ô'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('c', 'h'), 2)
**[Step 4] Merging pair ('c', 'h') (freq=2) -> 'ch'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('ch', 'à'), ('à', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n'), ('n', 'g'), ('g', '</w>')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('ch', 'à'), 2), (('à', 'o'), 2), (('o', '</w>'), 2), (('t', 'ô'), 2), (('ô', 'i'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('ch', 'à'), 2)
**[Step 5] Merging pair ('ch', 'à') (freq=2) -> 'chà'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('chà', 'o'), ('o', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n'), ('n', 'g'), ('g', '</w>'), ('b', 'ạ')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('chà', 'o'), 2), (('o', '</w>'), 2), (('t', 'ô'), 2), (('ô', 'i'), 2), (('i', '</w>'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('chà', 'o'), 2)
**[Step 6] Merging pair ('chà', 'o') (freq=2) -> 'chào'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('chào', '</w>'), ('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n'), ('n', 'g'), ('g', '</w>'), ('b', 'ạ'), ('ạ', 'n</w>')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('chào', '</w>'), 2), (('t', 'ô'), 2), (('ô', 'i'), 2), (('i', '</w>'), 2), (('n', 'g'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('chào', '</w>'), 2)
**[Step 7] Merging pair ('chào', '</w>') (freq=2) -> 'chào</w>'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('t', 'ô'), ('ô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n'), ('n', 'g'), ('g', '</w>'), ('b', 'ạ'), ('ạ', 'n</w>'), ('c', 'ó')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('t', 'ô'), 2), (('ô', 'i'), 2), (('i', '</w>'), 2), (('n', 'g'), 2), (('g', '</w>'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('t', 'ô'), 2)
**[Step 8] Merging pair ('t', 'ô') (freq=2) -> 'tô'**

--- [Step 3: Extract Bigrams] ---
Bigrams extracted from current token list (showing first 15):
 [('tô', 'i'), ('i', '</w>'), ('t', 'ê'), ('ê', 'n</w>'), ('l', 'à'), ('à', '</w>'), ('t', 'h'), ('h', 'ắ'), ('ắ', 'n'), ('n', 'g'), ('g', '</w>'), ('b', 'ạ'), ('ạ', 'n</w>'), ('c', 'ó'), ('ó', '</w>')]

--- [Step 4: Count Bigrams] ---
Top 5 bigram counts:
 [(('tô', 'i'), 2), (('i', '</w>'), 2), (('n', 'g'), 2), (('g', '</w>'), 2), (('b', 'ạ'), 2)]

--- [Step 5: Find Most Frequent Bigram] ---
Most frequent bigram:
 (('tô', 'i'), 2)
**[Step 9] Merging pair ('tô', 'i') (freq=2) -> 'tôi'**

=== Merges learned (in order) ===
(('n', '</w>'), 'n</w>')
(('k', 'h'), 'kh')
(('x', 'i'), 'xi')
(('xi', 'n</w>'), 'xin</w>')
(('c', 'h'), 'ch')
(('ch', 'à'), 'chà')
(('chà', 'o'), 'chào')
(('chào', '</w>'), 'chào</w>')
(('t', 'ô'), 'tô')
(('tô', 'i'), 'tôi')

=== Tokenized corpus after merges ===
['xin</w>']
['chào</w>']
['tôi', '</w>']
['t', 'ê', 'n</w>']
['l', 'à', '</w>']
['t', 'h', 'ắ', 'n', 'g', '</w>']
['b', 'ạ', 'n</w>']
['c', 'ó', '</w>']
['kh', 'ỏ', 'e', '</w>']
['kh', 'ô', 'n', 'g', '</w>']
['xin</w>']
['chào</w>']
['b', 'ạ', 'n</w>']
['tôi', '</w>']
['kh', 'ỏ', 'e', '</w>']

=== Vocab (Sample) ===
['</w>', 'b', 'c', 'chào</w>', 'e', 'g', 'h', 'kh', 'l', 'n', 'n</w>', 't', 'tôi', 'xin</w>', 'à', 'ê', 'ó', 'ô', 'ạ', 'ắ', 'ỏ']

Encoding text: 'xin chào thắng' ->
[['xin</w>'], ['chào</w>'], ['t', 'h', 'ắ', 'n', 'g', '</w>']]
```