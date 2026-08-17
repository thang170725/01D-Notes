- [Transformers Introduction](#transformers-introduction)
- [Installation](#installation)
- [AutoTokenizer (Biến văn bản -\> số, mỗi token sẽ được gán một số goi là ID. Trả về tensor.)](#autotokenizer-biến-văn-bản---số-mỗi-token-sẽ-được-gán-một-số-goi-là-id-trả-về-tensor)
- [AutoModelForCausalLM (mô hình Language Model sinh văn bản)](#automodelforcausallm-mô-hình-language-model-sinh-văn-bản)
  - [.from\_pretrained()](#from_pretrained)
    - [tokenizer() (biến text string → token IDs)](#tokenizer-biến-text-string--token-ids)
      - [.tokenize()](#tokenize)
      - [convert\_tokens\_to\_ids()](#convert_tokens_to_ids)
    - [.generate() (hàm sinh text dựa trên input)](#generate-hàm-sinh-text-dựa-trên-input)
      - [.decode (chuyển token IDs → string.)](#decode-chuyển-token-ids--string)
- [AutoModel](#automodel)
- [AutoModelForSequenceClassification (phân loại văn bản)](#automodelforsequenceclassification-phân-loại-văn-bản)
- [BertTokenizer \& BertModel](#berttokenizer--bertmodel)
- [Practices](#practices)
  - [Tính độ giống nhau bằng cosine sử dụng phoBert](#tính-độ-giống-nhau-bằng-cosine-sử-dụng-phobert)
  - [Demo AutoModel \& Auto Tokenizer](#demo-automodel--auto-tokenizer)
  - [So sánh độ giống nhau giữa 2 câu](#so-sánh-độ-giống-nhau-giữa-2-câu)
---
# Transformers Introduction
```bash
Transformers là một library được phát triển bởi Hugging Face.
    Là một trong những thư viện AI phổ biến nhất hiện nay.

Nó giúp bạn sử dụng các mô hình Transformer một cách đơn giản
```
**Phân loại mô hình theo task**
```bash
1. Mô hình sinh văn bản (Text Generation)

Đây là nhóm LLM mà mọi người thường nhắc đến.

Ứng dụng

Chatbot
AI Assistant
Viết code
Viết email
Viết bài
Agent

Ví dụ

GPT-2
Llama
Mistral
Mixtral
Qwen
Gemma
Falcon
BLOOM
OPT
Phi
GPT-Neo
GPT-J
GPT-NeoX

Ví dụ

from transformers import AutoModelForCausalLM
2. Mô hình Encoder (Embedding & Hiểu văn bản)

Nhóm này không giỏi viết mà giỏi hiểu.

Ứng dụng

Embedding
Semantic Search
RAG
Phân loại
Clustering

Ví dụ

BERT
RoBERTa
DeBERTa
DistilBERT
ALBERT
ELECTRA
MPNet
MiniLM

Ví dụ

AutoModel
3. Text Classification

Dùng để phân loại.

Ví dụ

Spam
Toxic
Positive
Negative
Chủ đề

Model thường dùng

BERT
RoBERTa
DistilBERT
DeBERTa

Ví dụ

AutoModelForSequenceClassification
4. Token Classification

Phân loại từng từ.

Ví dụ

Tôi sống ở Hà Nội

Tôi      O
sống     O
ở        O
Hà Nội   LOCATION

Ứng dụng

NER
POS Tagging

Model

BERT
RoBERTa
DeBERTa

Ví dụ

AutoModelForTokenClassification
5. Question Answering

Cho Context + Question.

Ví dụ

Context:
Việt Nam có thủ đô là Hà Nội.

Question:
Thủ đô Việt Nam là gì?

↓

Hà Nội

Model

BERT
RoBERTa
DistilBERT

Ví dụ

AutoModelForQuestionAnswering
6. Summarization

Tóm tắt.

Ví dụ

Báo chí
PDF
Email

Model

BART
T5
Pegasus
LongT5

Ví dụ

pipeline("summarization")
7. Translation

Dịch ngôn ngữ.

Ví dụ

Anh → Việt
Việt → Nhật

Model

MarianMT
mBART
M2M100
NLLB

Ví dụ

pipeline("translation")
8. Fill Mask

Điền từ bị thiếu.

Ví dụ

I love [MASK].

↓

Python

Model

BERT
RoBERTa
DeBERTa

Ví dụ

pipeline("fill-mask")
9. Sentence Embedding

Sinh vector.

Ứng dụng

RAG
Search
Recommendation

Model

BGE
E5
GTE
Sentence-BERT
MiniLM
10. Image Classification

Ảnh →

chó
mèo
xe

Model

ViT
ConvNext
Swin Transformer
BEiT

Ví dụ

AutoModelForImageClassification
11. Object Detection

Tìm vật thể.

Ví dụ

Ảnh

↓

Người

↓

Bounding Box

Model

DETR
YOLOS
DINO
12. Image Segmentation

Tách từng pixel.

Ví dụ

Người

Xe

Cây

Model

SegFormer
Mask2Former
SAM (một số phiên bản)
13. Image Captioning

Sinh mô tả ảnh.

Ví dụ

Ảnh

↓

"A dog running in a park."

Model

BLIP
BLIP-2
GIT
14. Visual Question Answering (VQA)

Ví dụ

Ảnh

+

"Có bao nhiêu người?"

↓

3 người

Model

BLIP
ViLT
15. Speech Recognition

Âm thanh →

Văn bản

Model

Whisper
Wav2Vec2
HuBERT
16. Text To Speech

Text →

Giọng nói

Model

Bark
SpeechT5
VITS
17. Audio Classification

Ví dụ

tiếng chó
tiếng còi
tiếng mưa

Model

AST
Wav2Vec2
18. Multimodal LLM

Đầu vào

Ảnh

+

Text

↓

Chat.

Model

LLaVA
Qwen2-VL
Phi-4 Multimodal
IDEFICS
SmolVLM
19. Code Generation

Sinh code.

Model

CodeLlama
StarCoder
CodeGen
DeepSeek-Coder
Qwen-Coder
20. Document AI

Hiểu PDF.

Model

LayoutLM
LayoutLMv2
LayoutLMv3
Donut
1. Qwen/Qwen2.5-7B-Instruct
2. Qwen/Qwen2.5-14B-Instruct
3. Qwen/Qwen2.5-72B-Instruct
4. mistralai/Mistral-7B-Instruct-v0.2
5. mistralai/Mixtral-8x7B-Instruct
6. meta-llama/Meta-Llama-3-8B-Instruct
7. meta-llama/Meta-Llama-3.1-8B-Instruct
8. google/gemma-2-9b-it
```
# Installation
```bash
1. pip install transformers
```
# AutoTokenizer (Biến văn bản -> số, mỗi token sẽ được gán một số goi là ID. Trả về tensor.)
```bash
tokenizer tự động tương thích với mô hình bạn tải về. Nó sẽ encode câu thành token IDs mà mô hình hiểu được và decode ngược lại thành text.
```
# AutoModelForCausalLM (mô hình Language Model sinh văn bản)
```bash
“Causal LM” = mô hình dự đoán token tiếp theo dựa trên các token trước (phù hợp cho chatbot, GPT).
```
**Syn**
```bash
model = AutoModelForCausalLM.from_pretrained(model_name)

- torch_dtype=torch.float16 → tiết kiệm RAM khi inference.
- device_map="auto" → phân phối mô hình sang GPU/CPU tự động.
```
**Ex**
```python
from transformers import AutoTokenizer, AutoModelForCausalLM
import torch

tokenizer = AutoTokenizer.from_pretrained("gpt2")
model = AutoModelForCausalLM.from_pretrained("gpt2")

prompt = "I am very hungry, so I want to"
inputs = tokenizer(prompt, return_tensors="pt")

outputs = model.generate(
    **inputs,
    max_length=30
)

print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```
## .from_pretrained()
```bash
from_pretrained() sẽ tải:
    1. Vocab/tokenizer config (SentencePiece, BPE, WordPiece…)
    2. Các thông số cần thiết để encode/decode.
```
**Syn**
```bash
tokenizer = AutoTokenizer.from_pretrained(model_name)

- model_name: tên mô hình/tokenizer trên Hub.
- use_fast=True/False → dùng Rust tokenizer (nhanh) hay Python.
- padding_side → trái/phải khi padding.
```
### tokenizer() (biến text string → token IDs)
**Syn**
```bash
inputs = tokenizer("### User: Xin chào\n### Assistant:", return_tensors="pt")

- Input:
    + return_tensors="pt" → trả về PyTorch tensor, nếu "tf" → TensorFlow.
    + padding=True → padding các câu trong batch về cùng độ dài.
    + truncation=True → cắt câu dài hơn max length của model.
- Output: list
```
**Ex**
```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")

text = "Tôi thích học AI."

inputs = tokenizer(text, return_tensors="pt")

print(inputs)
# Warning: You are sending unauthenticated requests to the HF Hub. Please set a HF_TOKEN to enable higher rate limits and faster downloads.
# {'input_ids': tensor([[    0,   218,   543,   222, 14877,     5,     2]]), 'attention_mask': tensor([[1, 1, 1, 1, 1, 1, 1]])}
```
#### .tokenize()
**Ex**
```python
from transformers import AutoTokenizer

# tải mô hình tiếng việt
tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")

# đoạn chữ muốn chuyển
text = "xin chào tất cả các bạn, tôi tên là lê đức thắng"

# chia đoạn text thành các token
tokens = tokenizer.tokenize(text, return_tensors="pt")
print(tokens) # ['xin', 'chào', 'tất', 'cả', 'các', 'bạ@@', 'n@@', ',', 'tôi', 'tên', 'là', 'lê', 'đức', 'thắng']
```
#### convert_tokens_to_ids()
**Ex**
```python
from transformers import AutoTokenizer

# tải mô hình tiếng việt
tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")

# đoạn chữ muốn chuyển
text = "xin chào tất cả các bạn, tôi tên là lê đức thắng"

# chia đoạn text thành các token
tokens = tokenizer.tokenize(text)
ids = tokenizer.convert_tokens_to_ids(tokens)
# in ra màn hình
print(tokens) # ['xin', 'chào', 'tất', 'cả', 'các', 'bạ@@', 'n@@', ',', 'tôi', 'tên', 'là', 'lê', 'đức', 'thắng']
print(ids) # [611, 3683, 7328, 94, 9, 18964, 1301, 4, 70, 221, 8, 8942, 7344, 616]
```
### .generate() (hàm sinh text dựa trên input)
**Syn**
```python
model = AutoModelForCausalLM.from_pretrained(model_name)
outputs = model.generate(**inputs, max_new_tokens=50)

- input_ids (ở đây mình dùng **inputs để unpack dictionary).
- max_new_tokens=50 → mô hình sẽ sinh tối đa 50 token mới.
- do_sample=True/False → sampling ngẫu nhiên hay greedy.
- temperature=0.7 → điều chỉnh ngẫu nhiên khi sampling.
- top_k, top_p → lọc token theo xác suất (nucleus/top-k sampling).
- outputs là tensor shape [1, N] → token IDs của cả input + output sinh ra.
```
#### .decode (chuyển token IDs → string.)
# AutoModel
# AutoModelForSequenceClassification (phân loại văn bản)
```python
from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained("distilbert-base-uncased", num_labels=2)

AutoModelForTokenClassification (gán nhãn từ NER)
from transformers import AutoModelForTokenClassification

model = AutoModelForTokenClassification.from_pretrained("dslim/bert-base-NER")
```
# BertTokenizer & BertModel
```python
from transformers import BertTokenizer, BertModel
import torch

tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")
model = BertModel.from_pretrained("bert-base-uncased")

sentence = "I am full"
inputs = tokenizer(sentence, return_tensors="pt")

with torch.no_grad():
    outputs = model(**inputs)

# Vector biểu diễn toàn câu là vector của token [CLS]
cls_embedding = outputs.last_hidden_state[0, 0]
print(cls_embedding.shape)  # torch.Size([768]), BERT chỉ trả về vector 768 chiều, không có phân loại, không có hỏi đáp.
```
# Practices
## Tính độ giống nhau bằng cosine sử dụng phoBert
```python
from transformers import AutoTokenizer, AutoModel
from sklearn.metrics.pairwise import cosine_similarity
import torch

# Load PhoBERT
tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")
model = AutoModel.from_pretrained("vinai/phobert-base")

# 3 câu cần so sánh
sentences = [
    "Tôi thích học trí tuệ nhân tạo.",
    "Tôi rất yêu AI.",
    "Hôm nay trời mưa."
]

embeddings = []

for sentence in sentences:
    inputs = tokenizer(sentence, return_tensors="pt")

    with torch.no_grad():
        outputs = model(**inputs)

    # Lấy embedding của token đầu tiên (<s>)
    sentence_embedding = outputs.last_hidden_state[:, 0, :]

    embeddings.append(sentence_embedding.squeeze().numpy())

# Tính độ giống nhau
similarity = cosine_similarity(embeddings)

print(similarity)
# [[1.0000001  0.57751805 0.52567667]
# [0.57751805 1.         0.6679814 ]
# [0.52567667 0.6679814  1.0000004 ]]
```
## Demo AutoModel & Auto Tokenizer
```python
from transformers import AutoModel, AutoTokenizer
import torch

# Khởi tạo tokenizer từ mô hình PhoBERT
tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")
# tải mô hình đã được huấn luyện sẵn về và lưu vào biến
model = AutoModel.from_pretrained("vinai/phobert-base")

# chuyển thành dạng số để mô hình hiểu được
inputs = tokenizer("bật nhạc lofi chill", return_tensors="pt")

# tắt chế độ học (training mode) để tiết kiệm tài nguyên và tăng tốc
with torch.no_grad():
    # đưa câu tensor vào mô hình phoBert để lấy vector ngữ nghĩa đầu ra
    outputs = model(**inputs)

# Trích xuất last_hidden_state: output của mỗi token
last_hidden_state = outputs.last_hidden_state  # shape: [batch_size, seq_len, hidden_size]

# Lấy vector của token đầu tiên (thường là token <s>) làm đại diện cho cả câu
sentence_vector = last_hidden_state[0][0]  # shape: [768]

# In ra kích thước và vector
print("Kích thước vector câu:", sentence_vector.shape)
print("Vector đại diện câu:")
print(sentence_vector)
```
## So sánh độ giống nhau giữa 2 câu
```python
from transformers import BertTokenizer, BertModel
import torch
import torch.nn.functional as F

tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")
model = BertModel.from_pretrained("bert-base-uncased")

sent_a = "I am full"
sent_b = "I already ate a lot"

def embed(sentence):
    inputs = tokenizer(sentence, return_tensors="pt")
    with torch.no_grad():
        outputs = model(**inputs)
    return outputs.last_hidden_state[0, 0]  # vector [CLS]

vec_a = embed(sent_a)
vec_b = embed(sent_b)

similarity = F.cosine_similarity(vec_a, vec_b, dim=0)
print("Cosine similarity:", similarity.item())

BertForSequenceClassification
from transformers import BertTokenizer, BertForSequenceClassification
import torch

tokenizer = BertTokenizer.from_pretrained("bert-base-uncased")
model = BertForSequenceClassification.from_pretrained("bert-base-uncased", num_labels=2)

text = "I feel great today!"
inputs = tokenizer(text, return_tensors="pt")

with torch.no_grad():
    outputs = model(**inputs)

logits = outputs.logits
pred = torch.argmax(logits, dim=1)
print("Predicted label:", pred.item()) # Đây là một tác vụ mà BERT THUẦN không làm được, phải dùng phiên bản “BERT + head cho phân loại”.
```