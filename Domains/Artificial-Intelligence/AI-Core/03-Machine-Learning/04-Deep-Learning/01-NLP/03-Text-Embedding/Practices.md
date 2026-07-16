# thực hành research Word2vec
```python
import numpy as np

# ==========================================================
# STEP 1 - Raw Text
# ==========================================================

text = "i love deep learning and i love nlp"

print("=" * 60)
print("STEP 1 - RAW TEXT")
print(text)

# ==========================================================
# STEP 2 - Tokenization
# ==========================================================

tokens = text.split()

print("\n" + "=" * 60)
print("STEP 2 - TOKENIZATION")

print(tokens)

# ==========================================================
# STEP 3 - Build Vocabulary
# ==========================================================

vocab = sorted(set(tokens))

print("\n" + "=" * 60)
print("STEP 3 - VOCABULARY")

print(vocab)

# ==========================================================
# STEP 4 - Word -> Token ID
# ==========================================================

word_to_id = {}

for idx, word in enumerate(vocab):
    word_to_id[word] = idx

print("\n" + "=" * 60)
print("STEP 4 - WORD -> TOKEN ID")

for word, idx in word_to_id.items():
    print(f"{word:10} ---> {idx}")

# ==========================================================
# STEP 5 - Token IDs
# ==========================================================

token_ids = [word_to_id[word] for word in tokens]

print("\n" + "=" * 60)
print("STEP 5 - SENTENCE TO TOKEN IDS")

print(token_ids)

# ==========================================================
# STEP 6 - Initialize Embedding Matrix
# ==========================================================

embedding_dim = 5

embedding_matrix = np.random.randn(
    len(vocab),
    embedding_dim
)

print("\n" + "=" * 60)
print("STEP 6 - RANDOM EMBEDDING MATRIX")

print("Shape:", embedding_matrix.shape)
print(embedding_matrix)

# ==========================================================
# STEP 7 - Lookup Embedding
# ==========================================================

print("\n" + "=" * 60)
print("STEP 7 - LOOKUP EMBEDDING")

for token_id in token_ids:

    vector = embedding_matrix[token_id]

    print(
        f"TokenID {token_id} "
        f"-> {vocab[token_id]:10}"
        f" -> {vector}"
    )

# ==========================================================
# STEP 8 - Final Pipeline
# ==========================================================

print("\n" + "=" * 60)
print("FULL PIPELINE")

for word in tokens:

    token_id = word_to_id[word]

    vector = embedding_matrix[token_id]

    print(f"""
Word      : {word}
Token ID  : {token_id}
Embedding :
{vector}
""")
```
```bash
============================================================
STEP 1 - RAW TEXT
i love deep learning and i love nlp

============================================================
STEP 2 - TOKENIZATION
['i', 'love', 'deep', 'learning', 'and', 'i', 'love', 'nlp']

============================================================
STEP 3 - VOCABULARY
['and', 'deep', 'i', 'learning', 'love', 'nlp']

============================================================
STEP 4 - WORD -> TOKEN ID
and        ---> 0
deep       ---> 1
i          ---> 2
learning   ---> 3
love       ---> 4
nlp        ---> 5

============================================================
STEP 5 - SENTENCE TO TOKEN IDS
[2, 4, 1, 3, 0, 2, 4, 5]

============================================================
STEP 6 - RANDOM EMBEDDING MATRIX
Shape: (6, 5)
[[ 1.26276575  0.76607755  0.35379382  0.74288746  0.90343547]
 [-1.46268815  0.80093222  0.72341375  0.20355631  1.1195029 ]
 [-0.12742463 -1.46116869  0.16558247  0.88145337 -0.74069513]
 [ 0.68810163  1.09942458  0.8063301  -0.22432766  0.17864732]
 [ 1.01762174  0.02299916 -0.43666352 -1.32938664 -1.23300914]
 [-0.15250007 -1.03981483 -0.25204862 -0.0760059  -1.0277791 ]]

============================================================
STEP 7 - LOOKUP EMBEDDING
TokenID 2 -> i          -> [-0.12742463 -1.46116869  0.16558247  0.88145337 -0.74069513]
TokenID 4 -> love       -> [ 1.01762174  0.02299916 -0.43666352 -1.32938664 -1.23300914]
TokenID 1 -> deep       -> [-1.46268815  0.80093222  0.72341375  0.20355631  1.1195029 ]
TokenID 3 -> learning   -> [ 0.68810163  1.09942458  0.8063301  -0.22432766  0.17864732]
TokenID 0 -> and        -> [1.26276575 0.76607755 0.35379382 0.74288746 0.90343547]
TokenID 2 -> i          -> [-0.12742463 -1.46116869  0.16558247  0.88145337 -0.74069513]
TokenID 4 -> love       -> [ 1.01762174  0.02299916 -0.43666352 -1.32938664 -1.23300914]
TokenID 5 -> nlp        -> [-0.15250007 -1.03981483 -0.25204862 -0.0760059  -1.0277791 ]

============================================================
FULL PIPELINE

Word      : i
Token ID  : 2
Embedding :
[-0.12742463 -1.46116869  0.16558247  0.88145337 -0.74069513]


Word      : love
Token ID  : 4
Embedding :
[ 1.01762174  0.02299916 -0.43666352 -1.32938664 -1.23300914]


Word      : deep
Token ID  : 1
Embedding :
[-1.46268815  0.80093222  0.72341375  0.20355631  1.1195029 ]


Word      : learning
Token ID  : 3
Embedding :
[ 0.68810163  1.09942458  0.8063301  -0.22432766  0.17864732]


Word      : and
Token ID  : 0
Embedding :
[1.26276575 0.76607755 0.35379382 0.74288746 0.90343547]


Word      : i
Token ID  : 2
Embedding :
[-0.12742463 -1.46116869  0.16558247  0.88145337 -0.74069513]


Word      : love
Token ID  : 4
Embedding :
[ 1.01762174  0.02299916 -0.43666352 -1.32938664 -1.23300914]


Word      : nlp
Token ID  : 5
Embedding :
[-0.15250007 -1.03981483 -0.25204862 -0.0760059  -1.0277791 ]
```