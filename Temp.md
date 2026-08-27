- [cbow temp](#cbow-temp)
---
1. PySpark là gì?

PySpark là Python API của Spark.

Spark ban đầu được xây dựng chủ yếu bằng Scala/Java.

PySpark cho phép bạn dùng Python để điều khiển Spark.

Ví dụ:

from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MyPipeline") \
    .getOrCreate()

df = spark.read.json("data.json")

df.filter(df.age > 18).show()

Nếu dùng Pandas:

import pandas as pd

df = pd.read_json("data.json")

df = df[df["age"] > 18]

Ý tưởng khá giống nhau.

Nhưng Spark có khả năng phân tán dữ liệu trên cluster.

# cbow temp
Nếu bạn muốn tự test CBOW/Word2Vec bằng Python, có vài lựa chọn. Với mục tiêu hiểu cơ chế, mình khuyên không nên dùng thư viện ngay từ đầu.

1. Muốn test nhanh → gensim

Thư viện phổ biến nhất cho Word2Vec là Gensim.

pip install gensim

Ví dụ:

from gensim.models import Word2Vec

sentences = [
    ["i", "love", "machine", "learning"],
    ["i", "love", "deep", "learning"],
    ["machine", "learning", "is", "interesting"],
    ["deep", "learning", "is", "powerful"],
]

model = Word2Vec(
    sentences,
    vector_size=100,
    window=2,
    min_count=1,
    sg=0,       # 0 = CBOW
    epochs=100
)

vector = model.wv["learning"]

print(vector)
print(model.wv.most_similar("learning"))

Điểm cần nhớ:

sg=0  # CBOW
sg=1  # Skip-gram
2. Nhưng nếu mục tiêu của bạn là hiểu CBOW

Mình khuyên bạn tự implement bằng PyTorch.

Ví dụ kiến trúc:

Context words
     ↓
Embedding
     ↓
Average
     ↓
Linear
     ↓
Softmax
     ↓
Target

Dùng:

pip install torch

Bạn sẽ tự thấy được:

embedding = nn.Embedding(vocab_size, embedding_dim)

và:

context_vector = embedding(context_words).mean(dim=0)

sau đó:

output = linear(context_vector)

rồi:

loss = CrossEntropyLoss()(output, target)

Train:

loss.backward()
optimizer.step()

Sau khi train:

embedding.weight

chính là nơi bạn có thể nhìn trực tiếp các vector mà model đã học.

3. Nếu học theo hướng của bạn, mình sẽ làm theo thứ tự
                CBOW
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
   Hiểu objective       Hiểu embedding
        │                   │
 Context → Target      Word → Vector
        │                   │
        └─────────┬─────────┘
                  ↓
            Tự code PyTorch
                  ↓
             Gensim test
                  ↓
             Skip-gram
                  ↓
              Word2Vec

Đừng bắt đầu bằng Gensim nếu mục tiêu là hiểu sâu. Gensim sẽ cho bạn kết quả rất nhanh nhưng bạn dễ chỉ biết sg=0 là CBOW mà chưa hiểu bên trong nó chạy thế nào.

Nếu muốn, mình có thể 
viết cho bạn một CBOW cực nhỏ bằng PyTorch, khoảng 30–40 dòng, rồi giải thích từng dòng từ input → embedding → average → predict target → backprop, khá hợp với hướng bạn đang học RNN/Seq2Seq.