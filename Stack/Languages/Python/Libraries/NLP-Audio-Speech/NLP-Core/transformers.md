Transformers
Mô hình cho chatbot Hỏi-Đáp:
    1. Qwen/Qwen2.5-7B-Instruct
    2. Qwen/Qwen2.5-14B-Instruct
    3. Qwen/Qwen2.5-72B-Instruct
    4. mistralai/Mistral-7B-Instruct-v0.2
    5. mistralai/Mixtral-8x7B-Instruct
    6. meta-llama/Meta-Llama-3-8B-Instruct
    7. meta-llama/Meta-Llama-3.1-8B-Instruct
    8. google/gemma-2-9b-it
AutoTokenizer
    • Biến văn bản thành số, mỗi token sẽ được gán một số goi là ID. Trả về tensor.
    • tokenizer tự động tương thích với mô hình bạn tải về. Nó sẽ encode câu thành token IDs mà mô hình hiểu được và decode ngược lại thành text.
Cú pháp:
tokenizer = AutoTokenizer.from_pretrained(model_name)
    • .from_pretrained() sẽ tải:
        1. Vocab/tokenizer config (SentencePiece, BPE, WordPiece…)
        2. Các thông số cần thiết để encode/decode.
    • Tham số chính:
        1. model_name: tên mô hình/tokenizer trên Hub.
        2. Có thể thêm:
            1. use_fast=True/False → dùng Rust tokenizer (nhanh) hay Python.
            2. padding_side → trái/phải khi padding.

AutoModel
AutoModelForSequenceClassification (phân loại văn bản)
from transformers import AutoModelForSequenceClassification

model = AutoModelForSequenceClassification.from_pretrained("distilbert-base-uncased", num_labels=2)

AutoModelForTokenClassification (gán nhãn từ NER)
from transformers import AutoModelForTokenClassification

model = AutoModelForTokenClassification.from_pretrained("dslim/bert-base-NER")

Bài tập
Ví dụ Demo AutoModel & Auto Tokenizer
from transformers import AutoModel, AutoTokenizer
# torch là thư viện Pytorch
import torch
# Khởi tạo tokenizer từ mô hình PhoBERT
tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")
# tải mô hình đã được huấn luyện sẵn về và lưu vào biến
model = AutoModel.from_pretrained("vinai/phobert-base")
#print(model)
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

BertTokenizer & BertModel
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
Bài tập
So sánh độ giống nhau giữa 2 câu
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
AutoModelForCausalLM
Dạng sinh văn bản. mô hình Language Model sinh văn bản (causal LM). “Causal LM” = mô hình dự đoán token tiếp theo dựa trên các token trước (phù hợp cho chatbot, GPT).
Cú pháp:
model = AutoModelForCausalLM.from_pretrained(model_name)
    • Tải trọng số pre-trained của mô hình.
    • AutoModelForCausalLM tự biết load mô hình dạng causal LM.
    • Tham số tùy chọn:
        ◦ torch_dtype=torch.float16 → tiết kiệm RAM khi inference.
        ◦ device_map="auto" → phân phối mô hình sang GPU/CPU tự động.


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
Bài tập 
Demo chatbot hỏi đáp
from transformers import AutoModelForCausalLM, AutoTokenizer

model_name = "mistralai/Mistral-7B-Instruct-v0.2"
tokenizer = AutoTokenizer.from_pretrained(model_name)
model = AutoModelForCausalLM.from_pretrained(model_name)

inputs = tokenizer("### User: Xin chào\n### Assistant:", return_tensors="pt")
outputs = model.generate(**inputs, max_new_tokens=50)
print(tokenizer.decode(outputs[0]))
Trainer
TrainingArguments
from_pretrained()
Để tải mô hình.
Mô hình:
    1. vinai/phobert-base
Tokenizer()
Cú pháp:
inputs = tokenizer("### User: Xin chào\n### Assistant:", return_tensors="pt")
    • tokenizer(...) biến text string → token IDs.
    • Tham số chính:
        ◦ return_tensors="pt" → trả về PyTorch tensor, nếu "tf" → TensorFlow.
        ◦ padding=True → padding các câu trong batch về cùng độ dài.
        ◦ truncation=True → cắt câu dài hơn max length của model.


inputs bây giờ là dictionary:
{
  'input_ids': tensor([[...]]),
  'attention_mask': tensor([[1, 1, 1, ...]])
}
input_ids → mã token.
attention_mask → 1 nếu token thực, 0 nếu padding.
.tokenize() & .convert_tokens_to_ids()
Để tách câu thành các token text hoặc token id.
Cú pháp:
from transformers import AutoTokenizer
# tải mô hình tiếng việt
tokenizer = AutoTokenizer.from_pretrained("vinai/phobert-base")
# đoạn chữ muốn chuyển
text = "xin chào tất cả các bạn, tôi tên là lê đức thắng"
# chia đoạn text thành các token
tokens = tokenizer.tokenize(text)
ids = tokenizer.convert_tokens_to_ids(tokens)
# in ra màn hình
print(tokens)
print(ids)
['xin', 'chào', 'tất', 'cả', 'các', 'bạ@@', 'n@@', ',', 'tôi', 'tên', 'là', 'lê', 'đức', 'thắng']
[611, 3683, 7328, 94, 9, 18964, 1301, 4, 70, 221, 8, 8942, 7344, 616]
.generate()
Cú pháp:
model = AutoModelForCausalLM.from_pretrained(model_name)
outputs = model.generate(**inputs, max_new_tokens=50)
    • model.generate() = hàm sinh text dựa trên input.
    • Tham số chính:
        ◦ input_ids (ở đây mình dùng **inputs để unpack dictionary).
        ◦ max_new_tokens=50 → mô hình sẽ sinh tối đa 50 token mới.
        ◦ Có thể thêm:
            ▪ do_sample=True/False → sampling ngẫu nhiên hay greedy.
            ▪ temperature=0.7 → điều chỉnh ngẫu nhiên khi sampling.
            ▪ top_k, top_p → lọc token theo xác suất (nucleus/top-k sampling).
            ▪ outputs là tensor shape [1, N] → token IDs của cả input + output sinh ra.
.decode
print(tokenizer.decode(outputs[0]))
    • tokenizer.decode() chuyển token IDs → string.
    • outputs[0] → tensor token của câu đầu tiên trong batch.
    • Optional parameters:
        ◦ skip_special_tokens=True → loại bỏ <s>, </s>, <pad>.

from_pretrained()
**input & .last_hiden_state()
Cú pháp:
from transformers import AutoTokenizer, AutoModel
import torch

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")
model = AutoModel.from_pretrained("bert-base-uncased")

inputs = tokenizer("Hello, how are you?", return_tensors="pt")
outputs = model(**inputs)

print(outputs.last_hidden_state.shape)  # (batch_size, seq_len, hidden_dim)
