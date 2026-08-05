- [Sentence Transformers Introduction](#sentence-transformers-introduction)
- [Installation](#installation)
- [Sentence Transformer Introduction](#sentence-transformer-introduction)
- [Installation](#installation-1)
- [Load model](#load-model)
- [Các câu](#các-câu)
- [Sinh embedding](#sinh-embedding)
- [So sánh độ giống nhau](#so-sánh-độ-giống-nhau)
---
# Sentence Transformers Introduction
[Kiến thức cơ bản về sentence transformers](../../../../../../../Domains/Artificial-Intelligence/AI-Core/03-Machine-Learning/04-Deep-Learning/01-NLP/04-Models/SBERT.md#sentence-bert-introduction-sbert-để-tạo-ra-vector-biểu-diễn-của-cả-câu-sentence-embedding)
# Installation
```bash
pip install sentence-transformers
```
Ví dụ 1: Mã hóa câu
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("all-MiniLM-L6-v2")

sentence = "Tôi thích học Python"

embedding = model.encode(sentence)

print(type(embedding))
print(len(embedding))
print(embedding[:10])    # 10 phần tử đầu

Ví dụ kết quả:

<class 'numpy.ndarray'>

384

[-0.12  0.54 -0.78 ...]

Model all-MiniLM-L6-v2 tạo vector có 384 chiều.

Ví dụ 2: So sánh hai câu
from sentence_transformers import SentenceTransformer
from sentence_transformers.util import cos_sim

model = SentenceTransformer("all-MiniLM-L6-v2")

s1 = "Tôi thích học Python"
s2 = "Tôi rất yêu lập trình Python"

e1 = model.encode(s1, convert_to_tensor=True)
e2 = model.encode(s2, convert_to_tensor=True)

score = cos_sim(e1, e2)

print(score)

Kết quả có thể:

tensor([[0.93]])

Điểm càng gần 1 thì hai câu càng giống nhau.

Ví dụ 3: Nhiều câu
from sentence_transformers import SentenceTransformer

model = SentenceTransformer("all-MiniLM-L6-v2")

sentences = [
    "Tôi thích học Python",
    "Tôi rất yêu lập trình Python",
    "Hôm nay trời mưa",
    "Tôi đi siêu thị"
]

embeddings = model.encode(sentences)

print(embeddings.shape)

Kết quả:

(4, 384)

Nghĩa là:

4 câu
Mỗi câu là một vector 384 chiều
Ví dụ 4: Tìm câu giống nhất
from sentence_transformers import SentenceTransformer
from sentence_transformers.util import cos_sim

model = SentenceTransformer("all-MiniLM-L6-v2")

docs = [
    "Tôi thích học Python",
    "Hôm nay trời đẹp",
    "Con mèo đang ngủ",
    "Python là ngôn ngữ lập trình"
]

query = "Tôi muốn học lập trình Python"

doc_embeddings = model.encode(docs, convert_to_tensor=True)
query_embedding = model.encode(query, convert_to_tensor=True)

scores = cos_sim(query_embedding, doc_embeddings)

print(scores)

Ví dụ:

tensor([[0.89, 0.18, 0.10, 0.85]])

Có thể lấy câu giống nhất:

best = scores.argmax()

print(docs[best])

Kết quả:

Tôi thích học Python
Ứng dụng của Sentence-BERT
Semantic Search: tìm kiếm theo ý nghĩa thay vì từ khóa.
Question Answering: tìm câu trả lời gần nghĩa nhất.
Document Retrieval: tìm tài liệu liên quan.
Phân cụm văn bản (Clustering).
Phát hiện câu trùng lặp (Duplicate Detection).
Hệ thống gợi ý (Recommendation) dựa trên nội dung.
BERT và Sentence-BERT khác nhau thế nào?
BERT	Sentence-BERT
Biểu diễn token hoặc câu nhưng chưa tối ưu cho so sánh	Tối ưu để tạo vector biểu diễn của cả câu
So sánh hai câu chậm (thường dùng cross-encoder)	So sánh rất nhanh bằng cosine similarity
Phù hợp cho phân loại, NER, QA	Phù hợp cho semantic search, tìm kiếm, clustering, retrieval
Khó dùng trực tiếp để tìm câu tương tự trong tập dữ liệu lớn	Chỉ cần mã hóa mỗi câu một lần rồi so sánh các vector

Nếu bạn đang học về MinHash LSH, thì Sentence-BERT thường được dùng để biểu diễn ngữ nghĩa của văn bản thành vector, sau đó có thể kết hợp với các kỹ thuật tìm kiếm gần đúng (ANN như FAISS hoặc HNSW) để tìm các câu tương tự rất nhanh trong tập dữ liệu lớn.
# Sentence Transformer Introduction
# Installation
```bash
1. pip install sentence-transformers
```
from sentence_transformers import SentenceTransformer
from sklearn.metrics.pairwise import cosine_similarity

# Load model
model = SentenceTransformer("all-MiniLM-L6-v2")

# Các câu
sentences = [
    "Tôi thích học trí tuệ nhân tạo.",
    "Tôi rất yêu AI.",
    "Hôm nay trời mưa."
]

# Sinh embedding
embeddings = model.encode(sentences)

# So sánh độ giống nhau
similarity = cosine_similarity(embeddings)

print(similarity)
(.venv) PS D:\workspace\test> python test.py
Warning: You are sending unauthenticated requests to the HF Hub. Please set a HF_TOKEN to enable higher rate limits and faster downloads.
modules.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 349/349 [00:00<?, ?B/s]
D:\workspace\test\.venv\Lib\site-packages\huggingface_hub\file_download.py:139: UserWarning: `huggingface_hub` cache-system uses symlinks by default to efficiently store duplicated files but your machine does not support them in C:\Users\thang.ld\.cache\huggingface\hub\models--sentence-transformers--all-MiniLM-L6-v2. Caching files will still work but in a degraded version that might require more space on your disk. This warning can be disabled by setting the `HF_HUB_DISABLE_SYMLINKS_WARNING` environment variable. For more details, see https://huggingface.co/docs/huggingface_hub/how-to-cache#limitations.
To support symlinks on Windows, you either need to activate Developer Mode or to run Python as an administrator. In order to activate developer mode, see this article: https://docs.microsoft.com/en-us/windows/apps/get-started/enable-your-device-for-development
  warnings.warn(message)
config_sentence_transformers.json: 100%|█████████████████████████████████████████████████████████████████████████████████████████████| 116/116 [00:00<?, ?B/s]
README.md: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████| 10.5k/10.5k [00:00<00:00, 10.2MB/s]
sentence_bert_config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████| 53.0/53.0 [00:00<?, ?B/s]
config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 612/612 [00:00<?, ?B/s]
model.safetensors: downloading bytes: ████████████████████████████████████████████████████████████████████████████████████████████████████| 85.0MB, 2.25MB/s  
model.safetensors: reconstructing file: 100%|████████████████████████████████████████████████████████████████████████████████████| 90.9MB / 90.9MB, 3.50MB/s  
Loading weights: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████| 103/103 [00:00<00:00, 2973.48it/s]
tokenizer_config.json: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████| 350/350 [00:00<?, ?B/s]
vocab.txt: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████| 232k/232k [00:00<00:00, 621kB/s]
tokenizer.json: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████| 466k/466k [00:00<00:00, 1.55MB/s]
special_tokens_map.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████| 112/112 [00:00<?, ?B/s]
config.json: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 190/190 [00:00<?, ?B/s]
[[1.        0.5026742 0.4886267]
 [0.5026742 0.9999998 0.5070527]
 [0.4886267 0.5070527 0.9999999]]
(.venv) PS D:\workspace\test> 
