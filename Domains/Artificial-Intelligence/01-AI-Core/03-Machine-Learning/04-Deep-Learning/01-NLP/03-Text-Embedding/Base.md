- [Embedding Introduction (vector ngữ nghĩa được học từ dữ liệu)](#embedding-introduction-vector-ngữ-nghĩa-được-học-từ-dữ-liệu)
- [Word2Vec (nhận token id của vocab -\> vector số embedding)](#word2vec-nhận-token-id-của-vocab---vector-số-embedding)
  - [CBOW (Continuous Bag of Words)](#cbow-continuous-bag-of-words)
  - [Skip-Gram](#skip-gram)
- [Glove (Global Vectors)](#glove-global-vectors)
- [FastText](#fasttext)
  - [N-gram](#n-gram)
- [nomic-embed-text](#nomic-embed-text)
- [OpenAI Embedding](#openai-embedding)
- [embeddings/openai\_embedding.py](#embeddingsopenai_embeddingpy)
- [embeddings/hf\_embedding.py](#embeddingshf_embeddingpy)
- [Practices](#practices)
  - [Demo Transformer Embedding](#demo-transformer-embedding)
---
# Embedding Introduction (vector ngữ nghĩa được học từ dữ liệu)
# Word2Vec (nhận token id của vocab -> vector số embedding)
```bash
Ý tưởng:
    Những từ xuất hiện trong ngữ cảnh giống nhau sẽ có vector gần nhau

Ví dụ:
    - Vua gần Hoàng hậu
    - Hà Nội gần TP.HCM

    Word2Vec học được:
        King - Man + Woman ≈ Queen

Dùng để:
    - Biểu diễn từ thành vector
    - Tìm từ đồng nghĩa
    - Làm input cho model NLP
```
## CBOW (Continuous Bag of Words)
```bash
Nhiệm vụ:
    Đoán từ ở giữa từ các từ xung quanh.

Ví dụ:
    Tôi ăn ___ vào buổi sáng

    Từ context:
        Tôi ăn ... vào buổi sáng
    Model đoán:
        phở

Dùng để train Word2Vec
```
## Skip-Gram 
```bash
Ngược với CBOW.

Nhiệm vụ:
    Dùng từ trung tâm để đoán các từ xung quanh.

Ví dụ:
    Tôi ăn phở vào buổi sáng

    Input:
        phở
    Output:
        ăn
        vào
        buổi
        sáng

Dùng để train Word2Vec.
```
# Glove (Global Vectors)
```bash
- Word2Vec:
    Nhìn từng câu
- GloVe:
    Nhìn toàn bộ thống kê corpus

Ví dụ đếm:
    King xuất hiện với Queen bao nhiêu lần

    Từ đó học embedding.

Dùng để:
    - Sinh word embedding
    - Từng rất phổ biến trước BERT
```
# FastText 
```bash
Do Meta AI phát triển.

Ý tưởng:
    Một từ được tạo từ nhiều n-gram ký tự.

Ví dụ:
    học
        Tách:
            <h
            họ
            ọc
            c>

Embedding từ: = tổng embedding các n-gram

Ưu điểm:
    - Hiểu từ hiếm
    - Hiểu từ chưa từng gặp (OOV)

Ví dụ:
    chatgptxyz

    Word2Vec:
        Không biết
    FastText:
        Đoán được nhờ các n-gram
```
## N-gram
```bash
Là chuỗi gồm N token liên tiếp.

Ví dụ:
    Câu: Tôi thích học NLP

Unigram (1-gram):
    Tôi
    thích
    học
    NLP

Bigram (2-gram):
    Tôi thích
    thích học
    học NLP

Trigram (3-gram):
    Tôi thích học
    thích học NLP

Dùng để:
    - Language Model cổ điển
    - FastText
    - Gợi ý từ tiếp theo
```
# nomic-embed-text
# OpenAI Embedding
Đúng câu hỏi này rất quan trọng nếu bạn đang làm AI/RAG/microservice. Điểm mấu chốt là:

OpenAI Embedding không phải là một loại embedding khác về bản chất.
Nó cũng là một model biến text → vector giống các embedding model trên Hugging Face. Khác nhau chủ yếu nằm ở model được train thế nào, chất lượng, kích thước vector, chi phí, tốc độ và cách triển khai.

OpenAI hiện cung cấp các embedding model như text-embedding-3-small và text-embedding-3-large.

1. Trước hết: Embedding thực chất là gì?

Ví dụ bạn có:

"Cách sử dụng Docker"

Embedding model biến nó thành một vector:

[
    0.021,
    -0.183,
    0.442,
    ...
]

Ví dụ giả sử vector có 5 chiều:

"Cách sử dụng Docker"
        ↓
[0.2, -0.7, 0.4, 0.1, 0.8]

Một câu khác:

"Hướng dẫn dùng Docker"
        ↓
[0.21, -0.69, 0.42, 0.09, 0.79]

Hai vector gần nhau → hai câu có ý nghĩa tương tự.

Đây chính là nền tảng của:

Semantic Search
RAG
Recommendation
Document Retrieval
Duplicate Detection
Clustering
Similarity Search

Hugging Face cũng mô tả feature extraction/embedding theo đúng hướng này: chuyển text thành vector để retrieval, reranking hoặc tính similarity giữa các câu.

2. Vậy OpenAI Embedding khác Hugging Face thế nào?

Hãy hình dung:

                 EMBEDDING
                     │
        ┌────────────┴────────────┐
        │                         │
     OpenAI                  Hugging Face
        │                         │
 text-embedding-3        BGE / E5 / GTE / ...
        │                         │
       API                    Local model
        │                         │
    Internet                GPU / CPU của bạn

Cả hai đều làm cùng một nhiệm vụ:

Text → Vector

Nhưng cách sử dụng khác nhau.

3. OpenAI Embedding

Ví dụ bạn dùng:

text-embedding-3-small

Kiến trúc ứng dụng:

Your Python application
        │
        │ HTTPS API
        ↓
OpenAI Embedding API
        │
        ↓
Embedding Model
        │
        ↓
Vector
        │
        ↓
Your application

Bạn không tải model về máy.

Bạn gửi:

text = "Docker là gì?"

OpenAI xử lý và trả về:

[
    0.012,
    -0.034,
    0.127,
    ...
]
Ví dụ Python

Bạn có thể sử dụng SDK của OpenAI:

from openai import OpenAI

client = OpenAI()

response = client.embeddings.create(
    model="text-embedding-3-small",
    input="Docker là gì?"
)

embedding = response.data[0].embedding

print(len(embedding))
print(embedding[:5])

Sau đó bạn lưu vector này vào:

Qdrant
Milvus
Pinecone
Weaviate
Chroma
pgvector
...
4. Còn Hugging Face thì sao?

Hugging Face giống như một kho model.

Có rất nhiều embedding model:

BAAI/bge-...
intfloat/e5-...
thenlper/gte-...
sentence-transformers/...
...

Ví dụ dùng Sentence Transformers:

from sentence_transformers import SentenceTransformer

model = SentenceTransformer("BAAI/bge-small-en-v1.5")

texts = [
    "Docker là gì?",
    "Cách sử dụng Docker"
]

embeddings = model.encode(texts)

print(embeddings.shape)

Ở đây:

model
  ↓
được download về máy
  ↓
CPU/GPU của bạn
  ↓
text → vector

Hugging Face cũng hỗ trợ inference qua API thay vì chạy local; tài liệu hiện tại cho phép gọi feature extraction qua InferenceClient.

5. Điểm khác biệt lớn nhất

Tôi nghĩ bạn nên nhớ bảng này:

	OpenAI Embedding	Hugging Face Embedding
Model	OpenAI cung cấp	Rất nhiều model
Chạy ở đâu	Cloud	Local hoặc cloud
Download model	❌	✅ nếu chạy local
GPU	Không cần quản lý	Có thể cần
API	Rất đơn giản	Tùy model/framework
Chi phí	Tính theo usage	Local thì chủ yếu là hạ tầng
Custom model	Hạn chế hơn	Rất linh hoạt
Offline	❌	✅
Privacy	Data gửi API	Có thể giữ toàn bộ local
Deployment	Dễ	Phức tạp hơn
Control	Thấp hơn	Cao hơn
6. Một điểm rất quan trọng: "Transformer model" không đồng nghĩa "Embedding model"

Đây là chỗ người mới rất dễ nhầm.

Ví dụ:

BERT
GPT
Llama
Qwen
Mistral
BGE
E5
GTE

đều có thể liên quan đến Transformer, nhưng không phải model nào cũng nên lấy output ra làm embedding.

Ví dụ:

BERT

ban đầu được thiết kế chủ yếu cho các NLP task.

Bạn có thể lấy:

hidden states

của BERT:

tokens
   ↓
Transformer
   ↓
hidden states
   ↓
[CLS]

rồi biến thành vector.

Nhưng điều đó không có nghĩa BERT là một embedding model tốt nhất cho semantic search.

7. Đây là lý do có các model chuyên về embedding

Ví dụ:

BGE
E5
GTE
Sentence-BERT

được train/finetune đặc biệt cho:

sentence similarity
semantic search
retrieval
embedding

Vì vậy:

BERT

và

BGE

đều là Transformer-based models.

Nhưng mục tiêu sử dụng khác nhau.

Có thể hình dung:

                Transformer
                     │
       ┌─────────────┴──────────────┐
       │                            │
   General NLP                 Embedding
       │                            │
     BERT                    BGE / E5 / GTE
       │                            │
 classification                similarity
 NER / QA / etc.               retrieval
8. Một điều còn quan trọng hơn: embedding model được train như thế nào

Đây mới là thứ quyết định embedding có tốt hay không.

Ví dụ ta muốn:

"How to install Docker?"

gần:

"Guide to installing Docker"

và xa:

"How to cook chicken?"

Model embedding được train để:

similar meaning
       ↓
vectors close

và:

different meaning
       ↓
vectors far

Có thể hình dung:

                    Vector Space

       Docker
         ●
        ● ●
       ●   ●
     installation
         

                           ●
                          ●
                       Cooking

Do đó embedding model không chỉ đơn giản là lấy hidden state của Transformer.

Chất lượng của embedding phụ thuộc rất nhiều vào objective/training data.

9. OpenAI Embedding nên hiểu như thế nào?

Bạn có thể coi:

text-embedding-3-small

là:

Một model embedding được OpenAI train và host sẵn, bạn chỉ cần gọi API.

Còn:

BAAI/bge-...
intfloat/e5-...
thenlper/gte-...

là:

Những embedding model mà bạn có thể lấy từ Hugging Face và tự chạy hoặc gọi inference provider.

10. Ví dụ thực tế với RAG

Giả sử bạn có 100.000 tài liệu.

Bạn chia chúng:

document
   ↓
chunking
   ↓
10.000 chunks

Sau đó embedding:

chunk 1
   ↓
embedding model
   ↓
vector 1

chunk 2
   ↓
embedding model
   ↓
vector 2

...

Lưu vào vector database:

Qdrant
    │
    ├── vector 1 + metadata
    ├── vector 2 + metadata
    ├── vector 3 + metadata
    └── ...

User hỏi:

"Làm thế nào để deploy model YOLO?"

Bạn embedding query:

query
 ↓
embedding model
 ↓
query vector

Sau đó:

query vector
      ↓
vector similarity search
      ↓
top-k chunks
      ↓
LLM
      ↓
answer

Đây chính là RAG.

11. Và có một quy tắc cực kỳ quan trọng

Document embedding và query embedding phải dùng cùng embedding model.

Ví dụ:

Documents
    ↓
OpenAI text-embedding-3-small
    ↓
vectors

thì query cũng:

Query
    ↓
OpenAI text-embedding-3-small
    ↓
vector

Không nên:

Documents → BGE
Query     → OpenAI

rồi đem vector so sánh trực tiếp.

Vì hai model tạo ra hai vector spaces khác nhau.

12. Vậy vector 1536 chiều có nghĩa gì?

Ví dụ một embedding model trả:

len(vector)

kết quả:

1536

thì:

text
 ↓
[ x1, x2, x3, ..., x1536 ]

Không nên hiểu:

x1 = "Docker"
x2 = "AI"
x3 = "Python"

Không phải vậy.

Các chiều không có ý nghĩa đơn giản kiểu:

dimension 1 = độ dài câu
dimension 2 = chủ đề
...

Nó là một distributed representation.

Nói đơn giản:

Ý nghĩa của câu được phân bố trên toàn bộ vector.

13. Cosine similarity

Sau khi có hai vector:

A = embedding("Docker là gì?")
B = embedding("Docker dùng để làm gì?")

ta tính similarity.

Thường dùng cosine similarity:

similarity(A, B)

Nếu:

0.95

→ rất giống về semantic.

Nếu:

0.10

→ rất khác.

Ví dụ Python:

from sklearn.metrics.pairwise import cosine_similarity

score = cosine_similarity(
    [embedding_a],
    [embedding_b]
)

print(score)
14. Vậy khi nào nên dùng OpenAI?

Nếu kiến trúc của bạn là kiểu:

app/
├── core/
├── config/
├── utils/
├── services/
├── pipelines/
└── main.py

thì tôi sẽ tách embedding thành service/module riêng.

Ví dụ:

app/
│
├── core/
│
├── config/
│
├── embeddings/
│   ├── openai_embedding.py
│   ├── hf_embedding.py
│   └── factory.py
│
├── vectorstores/
│   ├── qdrant.py
│   └── ...
│
├── pipelines/
│   └── rag_pipeline.py
│
└── main.py

Sau đó:

def embed_text(text: str):
    ...

Pipeline chỉ cần biết:

vector = embed_text(text)

chứ không cần quan tâm:

OpenAI?
BGE?
E5?
GTE?
15. Ví dụ kiến trúc rất hợp với cách bạn đang code

Bạn có thể abstraction như:

# embeddings/openai_embedding.py

def embed_text(text: str):
    ...

và:

# embeddings/hf_embedding.py

def embed_text(text: str):
    ...

Sau đó config:

EMBEDDING_PROVIDER = "openai"

Pipeline:

def run_rag_pipeline(query: str):

    query_vector = embed_text(query)

    documents = search_vector_db(query_vector)

    answer = generate_answer(
        query,
        documents
    )

    return answer

Như vậy bạn có thể đổi:

OpenAI
   ↓
BGE

mà không phải sửa RAG pipeline.

Đây chính là một ví dụ rất đẹp của cách bạn đang theo đuổi module + pipeline, không nhất thiết phải biến mọi thứ thành class.

16. Khi nào chọn OpenAI, khi nào chọn Hugging Face?
Chọn OpenAI nếu:
Muốn triển khai nhanh
        +
Không muốn quản GPU
        +
Muốn API đơn giản
        +
Chấp nhận gửi dữ liệu ra API
        +
Muốn tập trung vào application/RAG

Ví dụ:

Startup
POC
RAG production
Internal chatbot
Document search

rất tiện.

Chọn Hugging Face/local nếu:
Muốn chạy offline
        +
Dữ liệu nhạy cảm
        +
Có GPU
        +
Muốn kiểm soát model
        +
Muốn fine-tune
        +
Muốn tự tối ưu inference

Ví dụ:

Enterprise
On-premise
Private AI
Large-scale embedding
Custom domain
17. Có một điểm bạn nên đặc biệt chú ý khi làm tiếng Việt

Không phải:

model càng lớn
      ↓
embedding càng tốt

luôn đúng.

Bạn nên benchmark trên dataset thực tế của mình.

Ví dụ tài liệu của bạn là:

Vietnamese
technical documents
YOLO
AI
software engineering

thì nên thử vài model:

OpenAI embedding
BGE
E5
GTE
...

sau đó đo:

Recall@K
Precision@K
MRR
NDCG

thay vì chỉ nhìn model có bao nhiêu parameters.

18. Tóm lại bằng một sơ đồ

Bạn có thể nhớ thế này:

                         EMBEDDING
                             │
                 text → vector representation
                             │
             ┌───────────────┴───────────────┐
             │                               │
          OpenAI                         Hugging Face
             │                               │
     text-embedding-*               BGE / E5 / GTE / ...
             │                               │
          API call                     Local / API
             │                               │
       không quản GPU                 tự quản hạ tầng
             │                               │
             └───────────────┬───────────────┘
                             │
                          Vector
                             │
                             ↓
                       Vector Database
                             │
                 ┌───────────┴───────────┐
                 │                       │
             Qdrant                    pgvector
                 │
                 ↓
             Similarity Search
                 │
                 ↓
                RAG

Điểm quan trọng nhất: OpenAI Embedding và embedding model trên Hugging Face không khác nhau về khái niệm. Chúng đều giải bài toán text → semantic vector. Khác biệt chủ yếu là model/training + chất lượng + deployment + chi phí + quyền kiểm soát.

Nếu bạn đang học để xây RAG bằng Python theo kiến trúc app/core/utils/config/pipelines, bước tiếp theo rất đáng học là phân biệt LLM, Embedding Model, Reranker và Vector Database. Bốn thứ này thường bị trộn lẫn với nhau, nhưng khi hiểu rõ thì kiến trúc RAG sẽ sáng tỏ hẳn

vậy thì openAI embedding tốt hơn đúng không

Không hẳn. Nếu nói “dùng cho nhanh, ít phải vận hành, chất lượng tốt và ổn định” thì OpenAI thường là lựa chọn rất tốt. Nhưng không thể kết luận OpenAI luôn tốt hơn mọi embedding model trên Hugging Face.

Có thể hiểu như này:

Tiêu chí	OpenAI Embedding	Hugging Face
Chất lượng tổng thể	⭐⭐⭐⭐⭐	⭐⭐⭐⭐–⭐⭐⭐⭐⭐
Dễ sử dụng	⭐⭐⭐⭐⭐	⭐⭐⭐
Không cần GPU	✅	Nếu local thì tùy
Chạy offline	❌	✅
Tự kiểm soát model	Thấp	Cao
Fine-tune	Hạn chế	✅
Chi phí	API	Local có thể rẻ hơn
Triển khai nhanh	Rất tốt	Khá
Tùy biến	Thấp	Rất cao
Nếu mục tiêu của bạn là làm RAG

Ví dụ:

PDF
 ↓
chunk
 ↓
Embedding
 ↓
Vector DB
 ↓
Retriever
 ↓
LLM

thì OpenAI embedding là lựa chọn rất hợp lý để bắt đầu.

Bạn không phải lo:

CUDA
GPU memory
model quantization
batch inference
model loading
sentence-transformers

Chỉ cần:

response = client.embeddings.create(
    model="text-embedding-3-small",
    input=text
)

vector = response.data[0].embedding

Sau đó đưa vector vào Qdrant/pgvector/etc.

Nhưng có một trường hợp Hugging Face có thể tốt hơn

Giả sử bạn có một hệ thống:

100 triệu documents
        ↓
embedding hàng ngày
        ↓
hàng tỷ vectors

Lúc này chi phí API có thể trở thành vấn đề lớn.

Bạn có thể lấy một embedding model như BGE/E5 phù hợp, chạy GPU nội bộ:

                 GPU Server
                     │
              BGE / E5 model
                     │
       ┌─────────────┼─────────────┐
       ↓             ↓             ↓
    vector        vector        vector
       ↓             ↓             ↓
              Vector Database

Lúc đó Hugging Face/local có thể kinh tế và linh hoạt hơn rất nhiều.

Một điểm nữa: đừng chỉ nhìn "model nào mạnh hơn"

Với RAG, cái bạn thực sự cần quan tâm là:

Embedding quality
       ↓
Retrieval quality
       ↓
LLM nhận đúng context
       ↓
Answer quality

Ví dụ:

OpenAI
  ↓
Top 5 documents
  ↓
4/5 đúng

so với:

BGE
  ↓
Top 5 documents
  ↓
5/5 đúng

thì BGE tốt hơn cho chính bài toán RAG của bạn, dù OpenAI có thể mạnh hơn ở một số benchmark khác.

Nếu bạn mới xây hệ thống

Tôi sẽ khuyên đi theo hướng:

                 RAG
                  │
        ┌─────────┴─────────┐
        │                   │
    Embedding              LLM
        │                   │
     OpenAI             OpenAI / ...
        │
        ↓
   Vector Database
      Qdrant

Làm cho hệ thống chạy ổn trước.

Sau đó mới abstraction:

def embed_text(text):
    ...

và có thể thay:

OpenAI
   ↓
BGE
   ↓
E5

để benchmark.

Nói ngắn gọn: OpenAI không phải “embedding tốt nhất”, nhưng là một trong những lựa chọn dễ dùng và mạnh nhất để bắt đầu. Nếu mục tiêu của bạn là học và xây RAG bằng Python, tôi sẽ chọn OpenAI trước, sau đó mới thử BGE/E5 để hiểu sự khác biệt
# Practices
## Demo Transformer Embedding
```python
from typing import List, Dict, Tuple
from collections import Counter
import random as rnd
import torch
import math

class TransformerEmbedding:
    def __init__(self, vocab_size: int = 1000, d_model: int = 64, max_len: int = 32):
        self.vocab_size = vocab_size
        self.d_model = d_model
        self.max_len = max_len
        
        # Khởi tạo embedding matrix [vocab_size × d_model]
        # Đây là bảng tra cứu embedding của *toàn bộ từ vựng*
        self.embedding_matrix = torch.randn(vocab_size, d_model) * 0.01

    # =================================================================================
    # 1. Split sentence → tokens
    # =================================================================================
    def _split(self, sentence: str) -> List[str]:
        """
        Input:  "hello world NLP"
        Output: ["hello", "world", "NLP"]
        """
        return sentence.split()

    # =================================================================================
    # 2. Build vocabulary
    # =================================================================================
    def _counts_and_most(self, tokens: List[str], vocab_size: int) -> Dict[str, int]:
        """
        Input: tokens = ["hello","hello","world"], vocab_size=5
        Output: {"hello":0, "world":1, "<unk>":2}
        """
        counter = Counter(tokens)
        most = counter.most_common(vocab_size - 1)

        vocab = {tok: idx for idx, (tok, _) in enumerate(most)}
        vocab["<unk>"] = len(vocab)
        return vocab

    # =================================================================================
    # 3. Convert tokens → token_ids
    # =================================================================================
    def _token_id(self, text: str, vocab: Dict[str, int]) -> List[int]:
        """
        Input: "hello NLP"
        Output: [0, 2] nếu "hello":0 và "NLP":2 là <unk>
        """
        tokens = self._split(text)
        unk_id = vocab["<unk>"]
        return [vocab.get(tok, unk_id) for tok in tokens]

    # =================================================================================
    # 4. Padding sequences to max_len
    # =================================================================================
    def _padding_sequence(self, seqs: List[List[int]], max_len: int = 4) -> List[List[int]]:
        """
        Input: [[1,2,3], [4]]
        Output: [[1,2,3,0], [4,0,0,0]]
        """
        out = []
        for seq in seqs:
            if len(seq) < max_len:
                padded = seq + [0] * (max_len - len(seq))
            else:
                padded = seq[:max_len]
            out.append(padded)
        return out

    # =================================================================================
    # 5. Create attention mask
    # =================================================================================
    def _attention_mask(self, padded_seq: List[int]) -> List[int]:
        """
        Input: [1,2,0,0]
        Output: [1,1,0,0]
        """
        return [1 if x != 0 else 0 for x in padded_seq]

    # =================================================================================
    # 6. Random embedding matrix (chỉ dùng khi demo)
    # =================================================================================
    def _random_embedding(self, vocab_size: int, d_model: int) -> List[List[float]]:
        """
        Tạo embedding ngẫu nhiên để demo.
        """
        out = []
        for _ in range(vocab_size):
            r = [rnd.uniform(-0.1, 0.1) for _ in range(d_model)]
            out.append(r)
        return out

    # =================================================================================
    # 7. Lookup embedding for 1 token_id
    # =================================================================================
    def _lookup_embedding_for_one(self, token_id: int, embedding_matrix) -> List[float]:
        """
        Input: token_id=5
        Output: vectơ 1×d_model
        """
        return embedding_matrix[token_id]

    # =================================================================================
    # 8. Lookup embedding for a list of token_ids
    # =================================================================================
    def _lookup_embedding(self, token_ids: List[int], embedding_matrix) -> torch.Tensor:
        """
        Input: [2,5,9]
        Output: tensor (3 × d_model)
        """
        return torch.tensor([embedding_matrix[t] for t in token_ids], dtype=torch.float32)

    # =================================================================================
    # 9. Embed whole batch → vectorized (không for)
    # =================================================================================
    def _embedding_batch(self, batch: List[List[int]], embedding_matrix: torch.Tensor) -> torch.Tensor:
        """
        Input: [[1,2],[3,4]]
        Output: (batch_size=2, seq_len=2, d_model)
        """
        batch_tensor = torch.tensor(batch)            # (B, L)
        return embedding_matrix[batch_tensor]         # PyTorch tự broadcast → (B, L, D)

    # =================================================================================
    # 10. Positional Encoding (sin/cos)
    # =================================================================================
    def _positional_encoding(self, seq_len: int, d_model: int) -> torch.Tensor:
        """
        Output: (seq_len × d_model) matrix
        """
        position = torch.arange(seq_len).unsqueeze(1)  # (L,1)
        div_term = torch.exp(torch.arange(0, d_model, 2) * (-math.log(10000.0) / d_model))

        pe = torch.zeros(seq_len, d_model)
        pe[:, 0::2] = torch.sin(position * div_term)
        pe[:, 1::2] = torch.cos(position * div_term)
        return pe

    # =================================================================================
    # 11. Full Transformer Embedding = token embedding + positional encoding
    # =================================================================================
    def transformer_embedding(self, batch_token_ids: List[List[int]]) -> torch.Tensor:
        """
        Input: batch token IDs
        Output: (B, L, d_model) embedding sử dụng trong Transformer Encoder
        """

        # Step 1: padding
        padded = self._padding_sequence(batch_token_ids, self.max_len)  # (B, L)

        # Step 2: embed batch
        batch_emb = self._embedding_batch(padded, self.embedding_matrix)   # (B, L, D)

        # Step 3: positional encoding
        pe = self._positional_encoding(self.max_len, self.d_model)         # (L, D)

        # Step 4: add PE vào embedding (broadcast)
        final = batch_emb + pe                                             # (B, L, D)

        return final                   # embedding chính xác như trong Transformer


# ===============================================================================
# Demo chạy thử
# ===============================================================================
if __name__ == "__main__":
    te = TransformerEmbedding(vocab_size=10, d_model=8, max_len=4)

    # Demo batch token_ids
    batch = [
        [1, 2],
        [3, 4, 5]
    ]

    final_emb = te.transformer_embedding(batch)

    print("Transformer Embedding Output Shape:", final_emb.shape)
    print(final_emb)
```