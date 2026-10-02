- [vLLM Introduction](#vllm-introduction)
- [Installation](#installation)
- [Command line](#command-line)
  - [serve](#serve)
- [curl](#curl)
- [vllm](#vllm)
  - [LLM](#llm)
---
# vLLM Introduction
**Các thư viện Nên học trước**
[openai](Model-APIs/Openai/Base.md)

```bash
vLLM có thể gọi là thư viện Python, nhưng chính xác hơn, nó là một LLM inference/serving engine. Nó không phải framework kiểu Django/FastAPI.

Ví dụ bạn có model: Qwen, Llama, Mistral, ...
    vLLM chịu trách nhiệm load model lên GPU, nhận request, chạy inference và trả kết quả.
```
**Mục đích**
```bash
Mục đích chính của vLLM là: Chạy model LLM trên server và cung cấp API để các máy khác gửi request đến model.
```
**Architechture**
```bash
Máy công ty
    │
    │ HTTP request
    │ "Hãy tóm tắt email này"
    ▼
┌───────────────────────┐
│       Server          │
│                       │
│       vLLM            │
│         │             │
│         ▼             │
│       LLM             │
│                       │
└───────────────────────┘
    │
    ▼
  Kết quả
```
# Installation
**Linux**
```bash
1. pip install vllm
2. Kiểm tra: vllm --version
```
# Command line
## serve
**Syn**
```bash
vllm serve Qwen/Qwen3-8B \
    --port 8000 \
    --gpu-memory-utilization 0.9 # Nghĩa là cho vLLM sử dụng khoảng 90% GPU memory.
    --api-key my-secret-key # Sau đó client phải gửi: Authorization: Bearer my-secret-key
```
**Ex**
```bash
vllm serve Qwen/Qwen3-8B
# vllm serve
#     │
#     ├── load model
#     ├── load GPU
#     ├── tạo HTTP server
#     └── chờ request
```
# curl 
**Ex**
```bash
curl http://localhost:8000/v1/models
# {
#   "data": [
#     {
#       "id": "Qwen/Qwen3-8B"
#     }
#   ]
# }

curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen3-8B",
    "messages": [
      {
        "role": "user",
        "content": "Hãy tóm tắt email này: ..."
      }
    ]
  }'
```
# vllm
## LLM
```python
from vllm import LLM, SamplingParams

llm = LLM(
    model="Qwen/Qwen3-8B"
)

# cấu hình cách model sinh text
sampling_params = SamplingParams(
    temperature=0.7,
    max_tokens=200
)

# chạy inference
outputs = llm.generate(
    "Hãy tóm tắt email này",
    sampling_params
)

for output in outputs:
    print(output.outputs[0].text)
```

from openai import OpenAI

client = OpenAI(
    base_url="http://SERVER_IP:8000/v1",
    api_key="my-secret-key"
)

response = client.chat.completions.create(
    model="Qwen/Qwen3-8B",
    messages=[
        {
            "role": "user",
            "content": "Hãy tóm tắt email này..."
        }
    ]
)

print(response.choices[0].message.content)

Đây là mô hình client-server mà bạn đang hướng tới.

8. Tại sao lại dùng OpenAI Python SDK?

Điều này lúc đầu hơi dễ nhầm.

Không có nghĩa là:

Python application
       ↓
OpenAI

Mà là:

Python application
       ↓
OpenAI-compatible API
       ↓
vLLM
       ↓
Qwen/Llama/...

vLLM cung cấp API tương thích với OpenAI API.

Vì vậy bạn có thể dùng:

from openai import OpenAI

nhưng server phía sau lại là vLLM của bạn.

9. Các Linux command bạn sẽ dùng rất nhiều với vLLM
ls

Xem file:

ls

Chi tiết:

ls -lah
cd

Đi vào thư mục:

cd /home/user/llm

Quay lại:

cd ..
pwd

Xem thư mục hiện tại:

pwd
mkdir

Tạo thư mục:

mkdir models
cp

Copy:

cp file.txt backup.txt
mv

Di chuyển/đổi tên:

mv old.txt new.txt
rm

Xóa:

rm file.txt
cat

Xem nội dung:

cat config.json
less

Xem file dài:

less logfile.log
grep

Tìm kiếm:

grep "error" logfile.log
ps

Xem process:

ps aux

Tìm vLLM:

ps aux | grep vllm
kill

Dừng process:

kill PID
top

Theo dõi CPU/RAM:

top
nvidia-smi

Nếu server có NVIDIA GPU:

nvidia-smi

Đây là command cực kỳ quan trọng khi chạy vLLM.

Bạn có thể xem:

GPU
VRAM
GPU utilization
process đang sử dụng GPU
10. Các command liên quan trực tiếp đến server
Kiểm tra port 8000
ss -lntp | grep 8000
Kiểm tra API
curl http://localhost:8000/v1/models
Xem log

Nếu chạy trực tiếp:

vllm serve Qwen/Qwen3-8B

thì log xuất thẳng ra terminal.

Có thể redirect:

vllm serve Qwen/Qwen3-8B > vllm.log 2>&1

Sau đó:

tail -f vllm.log
11. Tóm lại, bạn cần nhớ 3 thứ
Tầng 1 — Linux
ls
cd
pwd
ps
kill
grep
tail
curl
nvidia-smi
Tầng 2 — vLLM server
vllm serve MODEL

Ví dụ:

vllm serve Qwen/Qwen3-8B \
    --port 8000 \
    --api-key my-secret-key
Tầng 3 — Application

Python:

from openai import OpenAI

client = OpenAI(
    base_url="http://SERVER_IP:8000/v1",
    api_key="my-secret-key"
)

Sau đó:

response = client.chat.completions.create(...)

Vậy nên vLLM không phải là nơi bạn viết toàn bộ application. Nó chủ yếu đóng vai trò inference server/engine, còn application của bạn gọi nó thông qua HTTP API.