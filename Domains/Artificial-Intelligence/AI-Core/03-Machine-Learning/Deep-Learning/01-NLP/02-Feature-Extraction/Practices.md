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