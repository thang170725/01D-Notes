- [Demo code thuần research BoW (Bag of Word)](#demo-code-thuần-research-bow-bag-of-word)
- [Demo code thuần research TF-IDF](#demo-code-thuần-research-tf-idf)
---
# Demo code thuần research BoW (Bag of Word)
```python
from collections import Counter

class BagOfWordsResearch:

    def __init__(self):
        self.documents = []
        self.tokenized_docs = []
        self.vocab = []
        self.word2idx = {}
        self.bow_matrix = []

    # ------------------------------------------------------
    # STEP 1
    # ------------------------------------------------------
    def add_documents(self, documents):

        print("=" * 60)
        print("STEP 1 - LOAD DOCUMENTS")
        print("=" * 60)

        self.documents = documents

        for i, doc in enumerate(documents):
            print(f"Document {i}: {doc}")

        print()

    # ------------------------------------------------------
    # STEP 2
    # ------------------------------------------------------
    def tokenize(self):

        print("=" * 60)
        print("STEP 2 - TOKENIZATION")
        print("=" * 60)

        self.tokenized_docs = []

        for i, doc in enumerate(self.documents):

            tokens = doc.lower().split()

            self.tokenized_docs.append(tokens)

            print(f"Document {i}")
            print("Original :", doc)
            print("Tokens   :", tokens)
            print()

    # ------------------------------------------------------
    # STEP 3
    # ------------------------------------------------------
    def build_vocab(self):

        print("=" * 60)
        print("STEP 3 - BUILD VOCABULARY")
        print("=" * 60)

        vocab_set = set()

        for tokens in self.tokenized_docs:

            for word in tokens:

                if word not in vocab_set:
                    print(f"Add new word -> {word}")

                vocab_set.add(word)

        self.vocab = sorted(list(vocab_set))

        print()
        print("Vocabulary")
        print(self.vocab)
        print()

    # ------------------------------------------------------
    # STEP 4
    # ------------------------------------------------------
    def create_mapping(self):

        print("=" * 60)
        print("STEP 4 - WORD TO INDEX")
        print("=" * 60)

        self.word2idx = {}

        for idx, word in enumerate(self.vocab):

            self.word2idx[word] = idx

            print(f"{word:15} ---> {idx}")

        print()

    # ------------------------------------------------------
    # STEP 5
    # ------------------------------------------------------
    def vectorize(self):

        print("=" * 60)
        print("STEP 5 - CREATE BAG OF WORDS")
        print("=" * 60)

        self.bow_matrix = []

        for doc_id, tokens in enumerate(self.tokenized_docs):

            print(f"\nProcessing Document {doc_id}")

            vector = [0] * len(self.vocab)

            print("Initial Vector")
            print(vector)
            print()

            counter = Counter(tokens)

            print("Word Frequency")
            print(counter)
            print()

            for word, count in counter.items():

                index = self.word2idx[word]

                print(
                    f"Word '{word}' appears {count} time(s) -> vector[{index}] = {count}"
                )

                vector[index] = count

            print()

            print("Final Vector")
            print(vector)

            self.bow_matrix.append(vector)

        print()

    # ------------------------------------------------------
    # STEP 6
    # ------------------------------------------------------
    def show_result(self):

        print("=" * 60)
        print("FINAL BAG OF WORDS MATRIX")
        print("=" * 60)

        print()

        print("Vocabulary Order")

        for i, word in enumerate(self.vocab):
            print(f"{i:2} : {word}")

        print()

        for i, vector in enumerate(self.bow_matrix):
            print(f"Document {i}")
            print(vector)
            print()

    # ------------------------------------------------------
    # RUN
    # ------------------------------------------------------
    def fit(self, documents):

        self.add_documents(documents)

        self.tokenize()

        self.build_vocab()

        self.create_mapping()

        self.vectorize()

        self.show_result()


if __name__ == "__main__":

    docs = [
        "I love cats",
        "I love dogs",
        "Dogs love bones",
        "Cats love fish",
        "I love love dogs"
    ]

    bow = BagOfWordsResearch()

    bow.fit(docs)
```
```bash
============================================================
STEP 1 - LOAD DOCUMENTS
============================================================
Document 0: I love cats
Document 1: I love dogs
Document 2: Dogs love bones
Document 3: Cats love fish
Document 4: I love love dogs

============================================================
STEP 2 - TOKENIZATION
============================================================
Document 0
Original : I love cats
Tokens   : ['i', 'love', 'cats']

Document 1
Original : I love dogs
Tokens   : ['i', 'love', 'dogs']

Document 2
Original : Dogs love bones
Tokens   : ['dogs', 'love', 'bones']

Document 3
Original : Cats love fish
Tokens   : ['cats', 'love', 'fish']

Document 4
Original : I love love dogs
Tokens   : ['i', 'love', 'love', 'dogs']

============================================================
STEP 3 - BUILD VOCABULARY
============================================================
Add new word -> i
Add new word -> love
Add new word -> cats
Add new word -> dogs
Add new word -> bones
Add new word -> fish

Vocabulary
['bones', 'cats', 'dogs', 'fish', 'i', 'love']

============================================================
STEP 4 - WORD TO INDEX
============================================================
bones           ---> 0
cats            ---> 1
dogs            ---> 2
fish            ---> 3
i               ---> 4
love            ---> 5

============================================================
STEP 5 - CREATE BAG OF WORDS
============================================================

Processing Document 0
Initial Vector
[0, 0, 0, 0, 0, 0]

Word Frequency
Counter({'i': 1, 'love': 1, 'cats': 1})

Word 'i' appears 1 time(s) -> vector[4] = 1
Word 'love' appears 1 time(s) -> vector[5] = 1
Word 'cats' appears 1 time(s) -> vector[1] = 1

Final Vector
[0, 1, 0, 0, 1, 1]

Processing Document 1
Initial Vector
[0, 0, 0, 0, 0, 0]

Word Frequency
Counter({'i': 1, 'love': 1, 'dogs': 1})

Word 'i' appears 1 time(s) -> vector[4] = 1
Word 'love' appears 1 time(s) -> vector[5] = 1
Word 'dogs' appears 1 time(s) -> vector[2] = 1

Final Vector
[0, 0, 1, 0, 1, 1]

Processing Document 2
Initial Vector
[0, 0, 0, 0, 0, 0]

Word Frequency
Counter({'dogs': 1, 'love': 1, 'bones': 1})

Word 'dogs' appears 1 time(s) -> vector[2] = 1
Word 'love' appears 1 time(s) -> vector[5] = 1
Word 'bones' appears 1 time(s) -> vector[0] = 1

Final Vector
[1, 0, 1, 0, 0, 1]

Processing Document 3
Initial Vector
[0, 0, 0, 0, 0, 0]

Word Frequency
Counter({'cats': 1, 'love': 1, 'fish': 1})

Word 'cats' appears 1 time(s) -> vector[1] = 1
Word 'love' appears 1 time(s) -> vector[5] = 1
Word 'fish' appears 1 time(s) -> vector[3] = 1

Final Vector
[0, 1, 0, 1, 0, 1]

Processing Document 4
Initial Vector
[0, 0, 0, 0, 0, 0]

Word Frequency
Counter({'love': 2, 'i': 1, 'dogs': 1})

Word 'i' appears 1 time(s) -> vector[4] = 1
Word 'love' appears 2 time(s) -> vector[5] = 2
Word 'dogs' appears 1 time(s) -> vector[2] = 1

Final Vector
[0, 0, 1, 0, 1, 2]

============================================================
FINAL BAG OF WORDS MATRIX
============================================================

Vocabulary Order
 0 : bones
 1 : cats
 2 : dogs
 3 : fish
 4 : i
 5 : love

Document 0
[0, 1, 0, 0, 1, 1]

Document 1
[0, 0, 1, 0, 1, 1]

Document 2
[1, 0, 1, 0, 0, 1]

Document 3
[0, 1, 0, 1, 0, 1]

Document 4
[0, 0, 1, 0, 1, 2]
```
# Demo code thuần research TF-IDF
```bash
import math
from collections import defaultdict


class TFIDFResearch:

    def __init__(self, corpus):
        """Khởi tạo class nghiên cứu TF-IDF với một tập văn bản (corpus)."""
        self.corpus = corpus
        self.documents_words = []  # Lưu danh sách từ của từng văn bản sau khi tách
        self.vocab = set()  # Lưu tập hợp tất cả các từ phân biệt (Từ điển)
        self.idf = {}  # Lưu giá trị IDF của từng từ

        print("=== BƯỚC 0: KHỞI TẠO TẬP VĂN BẢN (CORPUS) ===")
        for i, doc in enumerate(corpus):
            print(f" Văn bản {i+1}: '{doc}'")
        print("-" * 50)

    def pipeline(self):
        """Chạy toàn bộ quy trình xử lý dữ liệu của TF-IDF."""
        self._tokenize()
        self._calculate_idf()
        tfidf_matrix = self._calculate_tfidf_matrix()
        return tfidf_matrix

    def _tokenize(self):
        """Bước 1: Tách từ (Tokenization) và xây dựng từ điển."""
        print("\n=== BƯỚC 1: TÁCH TỪ (TOKENIZATION) ===")
        for i, doc in enumerate(self.corpus):
            # Chuyển về chữ thường và tách từ theo khoảng trắng
            words = doc.lower().split()
            self.documents_words.append(words)
            self.vocab.update(words)
            print(f" Văn bản {i+1} sau khi tách từ: {words}")

        print(f"\n=> Từ điển tổng hợp (Vocabulary) [{len(self.vocab)} từ]:")
        print(f"   {sorted(list(self.vocab))}")
        print("-" * 50)

    def _calculate_idf(self):
        """Bước 2: Tính giá trị IDF cho từng từ trong từ điển."""
        print("\n=== BƯỚC 2: TÍNH CƠ CHẾ HIẾM - IDF (INVERSE DOCUMENT FREQUENCY) ===")
        total_docs = len(self.corpus)
        print(f" Tổng số văn bản (N) = {total_docs}\n")

        # Đếm số văn bản chứa mỗi từ
        doc_count_per_word = defaultdict(int)
        for word in self.vocab:
            for doc_words in self.documents_words:
                if word in doc_words:
                    doc_count_per_word[word] += 1

        # Tính IDF theo công thức: log10(Tổng số văn bản / Số văn bản chứa từ)
        for word, count in doc_count_per_word.items():
            # Sử dụng log10 để số liệu giống ví dụ lý thuyết trước đó của chúng ta
            self.idf[word] = math.log10(total_docs / count)
            print(
                f" Từ '{word:7}': Xuất hiện ở {count}/{total_docs} văn bản -> IDF = log10({total_docs}/{count}) = {self.idf[word]:.3f}"
            )
        print("-" * 50)

    def _calculate_tfidf_matrix(self):
        """Bước 3: Tính toán ma trận TF-IDF cuối cùng."""
        print("\n=== BƯỚC 3: TÍNH TOÁN TF-IDF CHO TỪNG VĂN BẢN ===")
        tfidf_matrix = []

        for i, doc_words in enumerate(self.documents_words):
            print(f"\n--- Xử lý Văn bản {i+1}: {' '.join(doc_words)} ---")
            doc_len = len(doc_words)
            doc_tfidf = {}

            # Đếm số lần xuất hiện của các từ trong văn bản này để tính TF
            word_counts = defaultdict(int)
            for word in doc_words:
                word_counts[word] += 1

            # Tính TF-IDF cho từng từ xuất hiện trong văn bản
            for word in doc_words:
                tf = word_counts[word] / doc_len
                tfidf = tf * self.idf[word]
                doc_tfidf[word] = tfidf

                print(
                    f"  Từ '{word:7}': Count={word_counts[word]}, TF={word_counts[word]}/{doc_len}={tf:.2f} | IDF={self.idf[word]:.3f} => TF-IDF = {tfidf:.3f}"
                )

            # Chuyển đổi thành Vector dựa trên Từ điển (Vocab) để đưa về dạng ma trận số học giống như Machine Learning thực tế
            vector = []
            for word in sorted(list(self.vocab)):
                vector.append(round(doc_tfidf.get(word, 0.0), 3))

            tfidf_matrix.append(vector)
            print(
                f" => Vector số học đại diện cho Văn bản {i+1} (Theo thứ tự từ điển):"
            )
            print(f"    {vector}")

        print("=" * 50)
        return tfidf_matrix


# --- CHẠY THỬ NGHIỆM VỚI DỮ LIỆU CỤ THỂ ---
if __name__ == "__main__":
    # Tập dữ liệu mẫu mô phỏng từ ví dụ trước
    data_sample = ["Tôi thích học AI", "Tôi thích ăn kem", "Học AI rất vui"]

    # Khởi tạo đối tượng nghiên cứu
    research = TFIDFResearch(corpus=data_sample)

    # Chạy pipeline xử lý dữ liệu và xuất log
    final_matrix = research.pipeline()

    print("\n[KẾT QUẢ CUỐI CÙNG] Ma trận TF-IDF thu được để nạp vào Model:")
    for row in final_matrix:
        print(row)
```
```bash
=== BƯỚC 0: KHỞI TẠO TẬP VĂN BẢN (CORPUS) ===
 Văn bản 1: 'Tôi thích học AI'
 Văn bản 2: 'Tôi thích ăn kem'
 Văn bản 3: 'Học AI rất vui'
--------------------------------------------------

=== BƯỚC 1: TÁCH TỪ (TOKENIZATION) ===
 Văn bản 1 sau khi tách từ: ['tôi', 'thích', 'học', 'ai']
 Văn bản 2 sau khi tách từ: ['tôi', 'thích', 'ăn', 'kem']
 Văn bản 3 sau khi tách từ: ['học', 'ai', 'rất', 'vui']

=> Từ điển tổng hợp (Vocabulary) [8 từ]:
   ['ai', 'học', 'kem', 'rất', 'thích', 'tôi', 'vui', 'ăn']
--------------------------------------------------

=== BƯỚC 2: TÍNH CƠ CHẾ HIẾM - IDF (INVERSE DOCUMENT FREQUENCY) ===
 Tổng số văn bản (N) = 3

 Từ 'thích  ': Xuất hiện ở 2/3 văn bản -> IDF = log10(3/2) = 0.176
 Từ 'rất    ': Xuất hiện ở 1/3 văn bản -> IDF = log10(3/1) = 0.477
 Từ 'học    ': Xuất hiện ở 2/3 văn bản -> IDF = log10(3/2) = 0.176
 Từ 'kem    ': Xuất hiện ở 1/3 văn bản -> IDF = log10(3/1) = 0.477
 Từ 'ai     ': Xuất hiện ở 2/3 văn bản -> IDF = log10(3/2) = 0.176
 Từ 'tôi    ': Xuất hiện ở 2/3 văn bản -> IDF = log10(3/2) = 0.176
 Từ 'ăn     ': Xuất hiện ở 1/3 văn bản -> IDF = log10(3/1) = 0.477
 Từ 'vui    ': Xuất hiện ở 1/3 văn bản -> IDF = log10(3/1) = 0.477
--------------------------------------------------

=== BƯỚC 3: TÍNH TOÁN TF-IDF CHO TỪNG VĂN BẢN ===

--- Xử lý Văn bản 1: tôi thích học ai ---
  Từ 'tôi    ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'thích  ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'học    ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'ai     ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
 => Vector số học đại diện cho Văn bản 1 (Theo thứ tự từ điển):
    [0.044, 0.044, 0.0, 0.0, 0.044, 0.044, 0.0, 0.0]

--- Xử lý Văn bản 2: tôi thích ăn kem ---
  Từ 'tôi    ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'thích  ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'ăn     ': Count=1, TF=1/4=0.25 | IDF=0.477 => TF-IDF = 0.119
  Từ 'kem    ': Count=1, TF=1/4=0.25 | IDF=0.477 => TF-IDF = 0.119
 => Vector số học đại diện cho Văn bản 2 (Theo thứ tự từ điển):
    [0.0, 0.0, 0.119, 0.0, 0.044, 0.044, 0.0, 0.119]

--- Xử lý Văn bản 3: học ai rất vui ---
  Từ 'học    ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'ai     ': Count=1, TF=1/4=0.25 | IDF=0.176 => TF-IDF = 0.044
  Từ 'rất    ': Count=1, TF=1/4=0.25 | IDF=0.477 => TF-IDF = 0.119
  Từ 'vui    ': Count=1, TF=1/4=0.25 | IDF=0.477 => TF-IDF = 0.119
 => Vector số học đại diện cho Văn bản 3 (Theo thứ tự từ điển):
    [0.044, 0.044, 0.0, 0.119, 0.0, 0.0, 0.119, 0.0]
==================================================

[KẾT QUẢ CUỐI CÙNG] Ma trận TF-IDF thu được để nạp vào Model:
[0.044, 0.044, 0.0, 0.0, 0.044, 0.044, 0.0, 0.0]
[0.0, 0.0, 0.119, 0.0, 0.044, 0.044, 0.0, 0.119]
[0.044, 0.044, 0.0, 0.119, 0.0, 0.0, 0.119, 0.0]
```


import re
import math
from collections import Counter, defaultdict


# =====================================================
# 1. DATASET: 20 EMAIL ĐÃ CÓ NHÃN
# =====================================================

dataset = [
    # 10 email yêu cầu bồi thường
    ("Tôi muốn yêu cầu bồi thường bảo hiểm", "BOI_THUONG"),
    ("Tôi gửi hồ sơ bồi thường bảo hiểm", "BOI_THUONG"),
    ("Vui lòng xử lý hồ sơ yêu cầu bồi thường", "BOI_THUONG"),
    ("Tôi cần hướng dẫn thủ tục bồi thường", "BOI_THUONG"),
    ("Hồ sơ bồi thường của tôi đã được gửi", "BOI_THUONG"),
    ("Tôi muốn kiểm tra tiến độ bồi thường", "BOI_THUONG"),
    ("Xin hướng dẫn thủ tục yêu cầu bồi thường", "BOI_THUONG"),
    ("Tôi gửi giấy tờ liên quan đến bồi thường", "BOI_THUONG"),
    ("Vui lòng xác nhận hồ sơ bồi thường bảo hiểm", "BOI_THUONG"),
    ("Tôi cần hỗ trợ giải quyết yêu cầu bồi thường", "BOI_THUONG"),

    # 10 email yêu cầu hủy hợp đồng
    ("Tôi muốn hủy hợp đồng bảo hiểm", "HUY_HOP_DONG"),
    ("Xin hướng dẫn thủ tục hủy hợp đồng", "HUY_HOP_DONG"),
    ("Tôi gửi yêu cầu hủy hợp đồng bảo hiểm", "HUY_HOP_DONG"),
    ("Vui lòng xác nhận việc hủy hợp đồng", "HUY_HOP_DONG"),
    ("Tôi muốn chấm dứt hợp đồng bảo hiểm", "HUY_HOP_DONG"),
    ("Đề nghị xử lý hồ sơ hủy hợp đồng", "HUY_HOP_DONG"),
    ("Tôi cần mẫu đơn hủy hợp đồng bảo hiểm", "HUY_HOP_DONG"),
    ("Xin xác nhận yêu cầu chấm dứt hợp đồng", "HUY_HOP_DONG"),
    ("Tôi muốn biết quy trình hủy hợp đồng", "HUY_HOP_DONG"),
    ("Vui lòng hỗ trợ thủ tục chấm dứt hợp đồng", "HUY_HOP_DONG"),
]


# =====================================================
# 2. TẠO N-GRAM
# =====================================================

def tokenize(text):
    """
    Tách từ đơn giản bằng regex.
    Giữ chữ cái tiếng Việt và chữ số.
    """
    return re.findall(r"\w+", text.lower(), flags=re.UNICODE)


def create_ngrams(text, n=2):
    """
    Tạo N-gram từ văn bản.

    n=1: Unigram
    n=2: Bigram
    n=3: Trigram
    """
    words = tokenize(text)

    return [
        tuple(words[i:i+n])
        for i in range(len(words) - n + 1)
    ]


# Có thể đổi thành 1 hoặc 3 để thử nghiệm
N = 2


# =====================================================
# 3. HUẤN LUYỆN MÔ HÌNH NAIVE BAYES
# =====================================================

class NgramNaiveBayes:

    def __init__(self, n=2, alpha=1.0):
        self.n = n
        self.alpha = alpha

        # Tổng số email thuộc từng lớp
        self.class_doc_counts = Counter()

        # Đếm số lần từng N-gram xuất hiện trong mỗi lớp
        self.ngram_counts = defaultdict(Counter)

        # Tổng số N-gram của mỗi lớp
        self.total_ngrams = Counter()

        # Tập N-gram đã học từ dữ liệu train
        self.vocabulary = set()

        self.classes = []

    def fit(self, dataset):
        """
        Học từ dataset gồm các cặp:
        (nội dung email, nhãn)
        """

        for text, label in dataset:

            # Đếm số email thuộc lớp này
            self.class_doc_counts[label] += 1

            # Tạo N-gram cho email
            grams = create_ngrams(text, self.n)

            # Học tần suất N-gram theo nhãn
            for gram in grams:
                self.ngram_counts[label][gram] += 1
                self.total_ngrams[label] += 1
                self.vocabulary.add(gram)

        self.classes = list(self.class_doc_counts.keys())

        return self

    def predict(self, text):
        """
        Tính điểm log xác suất cho từng lớp,
        sau đó chọn lớp có điểm cao nhất.
        """

        grams = create_ngrams(text, self.n)

        # Chỉ sử dụng N-gram đã xuất hiện trong tập train
        grams = [g for g in grams if g in self.vocabulary]

        scores = {}

        total_docs = sum(self.class_doc_counts.values())
        vocab_size = len(self.vocabulary)

        for label in self.classes:

            # Xác suất tiên nghiệm P(class)
            prior = (
                self.class_doc_counts[label] / total_docs
            )

            score = math.log(prior)

            # Tính xác suất từng N-gram theo lớp
            for gram in grams:

                count = self.ngram_counts[label][gram]

                # Laplace smoothing để tránh xác suất bằng 0
                probability = (
                    count + self.alpha
                ) / (
                    self.total_ngrams[label]
                    + self.alpha * vocab_size
                )

                # Cộng log xác suất
                score += math.log(probability)

            scores[label] = score

        predicted_label = max(scores, key=scores.get)

        return predicted_label, scores, grams


# =====================================================
# 4. TRAIN
# =====================================================

model = NgramNaiveBayes(n=N)
model.fit(dataset)

print("SỐ EMAIL TRAIN:", len(dataset))
print("N-GRAM:", N)
print("KÍCH THƯỚC VOCABULARY:", len(model.vocabulary))

print("\nMỘT SỐ N-GRAM ĐÃ HỌC:")

for label in model.classes:
    print(f"\nLớp {label}:")

    for gram, count in model.ngram_counts[label].most_common(10):
        print(f"  {' '.join(gram):35s} xuất hiện {count} lần")


# =====================================================
# 5. TEST VỚI EMAIL CHƯA TỪNG XUẤT HIỆN TRONG TRAIN
# =====================================================

test_email = """
Kính gửi bộ phận bảo hiểm,
Tôi gửi hồ sơ và muốn yêu cầu bồi thường bảo hiểm.
Vui lòng hướng dẫn xử lý hồ sơ.
"""

prediction, scores, matched_ngrams = model.predict(test_email)

print("\n" + "=" * 50)
print("EMAIL TEST:")
print(test_email)

print("\nN-GRAM TEST ĐÃ TÌM THẤY TRONG VOCABULARY:")
for gram in matched_ngrams:
    print(" ", " ".join(gram))

print("\nĐIỂM LOG XÁC SUẤT:")
for label, score in scores.items():
    print(f"  {label}: {score:.4f}")

print("\nKẾT QUẢ DỰ ĐOÁN:", prediction)
