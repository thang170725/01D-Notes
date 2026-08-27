LoRA (Low-Rank Adaptation) là một kỹ thuật fine-tuning model lớn nhưng không cập nhật toàn bộ trọng số của model.

Nói ngắn gọn:

LoRA = đóng băng model gốc + chèn một lượng nhỏ tham số trainable để model học nhiệm vụ mới.

Đây là một kỹ thuật PEFT (Parameter-Efficient Fine-Tuning).

1. Vấn đề LoRA muốn giải quyết

Giả sử bạn có model:

Llama
7 billion parameters

Bạn muốn fine-tune nó cho:

general LLM
      ↓
customer-support chatbot

Fine-tuning truyền thống:

7B parameters
     ↓
update toàn bộ
     ↓
7B parameters phải train

Điều này rất tốn:

GPU VRAM
thời gian
storage
memory

LoRA nói:

"Không cần sửa toàn bộ 7B parameters. Tôi chỉ học một phần nhỏ để model thích nghi."

2. Cơ chế LoRA

Giả sử trong model có một weight matrix:

W

Fine-tuning bình thường:

W → W + ΔW

Trong đó:

ΔW

là thay đổi mà quá trình training học được.

Vấn đề là ΔW có thể rất lớn.

LoRA giả sử rằng:

Thay đổi cần thiết ΔW có thể được biểu diễn bằng một ma trận low-rank.

Nó phân rã:

ΔW = B × A

Trong đó:

W
│
├── frozen
│
└── LoRA
      A
      ↓
      B

Khi inference:

W' = W + B × A
3. Tại sao gọi là "Low-Rank"?

Ví dụ weight:

W: 4096 × 4096

Nếu train trực tiếp:

4096 × 4096
= 16,777,216 parameters

LoRA có thể chọn:

r = 8

và dùng:

A: 8 × 4096
B: 4096 × 8

Số parameter:

8 × 4096 + 4096 × 8
= 65,536

So sánh:

Full fine-tuning
16,777,216 parameters

LoRA
65,536 parameters

=> ít hơn rất nhiều.

Đây chính là sức mạnh của LoRA.

4. Workflow LoRA

Giả sử bạn có:

Llama
   ↓
pretrained model

và dataset:

Question → Answer

Workflow:

              PRETRAINED MODEL
                     │
                     ↓
              Freeze weights
                     │
          ┌──────────┴──────────┐
          │                     │
       Original W           LoRA A/B
       frozen               trainable
          │                     │
          │                     ↓
          │                 update A/B
          │                     │
          └──────────┬──────────┘
                     ↓
                W + BA
                     ↓
                  output

Trong training:

W
│
└── ❌ không update

A
│
└── ✅ update

B
│
└── ✅ update
5. Ví dụ thực tế

Bạn có model:

Qwen

Model gốc biết:

"How do I reset my password?"

nhưng bạn muốn nó trả lời theo format công ty:

Customer:
How do I reset my password?

Assistant:
To reset your password:
1. Open Settings
2. Select Security
3. Click Reset Password

Dataset:

instruction → response

LoRA sẽ học cách model nên thích nghi với style/task mới, thay vì học lại toàn bộ kiến thức của model.

6. Sau khi train bạn có gì?

Có:

Base Model
+
LoRA Adapter

Ví dụ:

Qwen 7B
   +
customer_support_adapter

Adapter có thể chỉ vài MB hoặc vài trăm MB tùy model/rank/các layer được target, trong khi model gốc có thể hàng GB.

Điểm rất hay:

Bạn có thể dùng một base model + nhiều LoRA adapter:

                   Qwen 7B
                      │
       ┌──────────────┼──────────────┐
       ↓              ↓              ↓
   medical        finance       customer
    LoRA             LoRA          LoRA

Không cần lưu 3 bản full model.

7. LoRA khác fine-tuning bình thường
Full fine-tuning
Base Model
    ↓
update tất cả weights
    ↓
New Model
LoRA
Base Model
    ↓
freeze
    ↓
train adapter
    ↓
Base Model + LoRA
	Full Fine-tuning	LoRA
Base weights update	✅	❌
Trainable parameters	Rất nhiều	Rất ít
VRAM	Cao	Thấp hơn
Training	Nặng	Nhẹ hơn
Adapter riêng	❌	✅
Nhiều task	Tốn storage	Rất tiện
Chất lượng	Có thể rất cao	Thường rất tốt
8. LoRA có phải "thay đổi source code model" không?

Không.

Điểm này liên quan đúng với chuyện bạn từng hỏi về fine-tuning.

Bạn không cần sửa source code kiểu:

# sửa architecture của Llama

Thay vào đó, về ý tưởng:

Original model
     ↓
   frozen
     +
LoRA matrices
     ↓
training

Bạn đang học thêm parameters, chứ không sửa source code của model.

9. QLoRA là gì?

Bạn sẽ gặp thuật ngữ này ngay sau LoRA.

QLoRA = Quantization + LoRA

Ví dụ:

Llama 7B
   ↓
quantize 4-bit
   ↓
giảm memory
   ↓
LoRA adapter
   ↓
train

Khác biệt:

LoRA
Base model: thường giữ precision cao hơn

QLoRA
Base model: quantized
LoRA adapter: trainable

QLoRA rất phổ biến khi muốn fine-tune LLM trên GPU có VRAM hạn chế.

10. Một cách nhớ rất dễ

Hãy tưởng tượng model là một chiếc xe:

Base model = chiếc xe hoàn chỉnh

Bạn muốn dùng nó cho địa hình mới.

Full fine-tuning
Tháo xe ra
↓
sửa rất nhiều bộ phận
↓
lắp lại
LoRA
Giữ nguyên chiếc xe
↓
gắn thêm một bộ kit nhỏ
↓
phù hợp địa hình mới

Model gốc vẫn còn nguyên.

Và đặt LoRA vào bức tranh bạn đang học

Bạn có thể nhìn chuỗi này:

Pretraining
     ↓
Base Model
     ↓
Fine-tuning
     │
     ├── Full Fine-tuning
     │
     └── PEFT
          │
          ├── LoRA
          ├── QLoRA
          └── các phương pháp khác

LoRA không phải một model mới, mà là một phương pháp để fine-tune model hiệu quả hơn về số lượng parameter và tài nguyên.

Nếu bạn đang muốn hiểu sâu AI thay vì chỉ biết "cách chạy fine-tune", thì phần đáng học tiếp theo là 
tại sao ΔW lại có thể được xấp xỉ bằng BA với rank thấp, và 
LoRA thường chèn vào q_proj, k_proj, v_proj, o_proj của Transformer như thế nào. Đó mới là phần giúp bạn hiểu bản chất LoRA chứ không chỉ biết dùng thư viện peft.