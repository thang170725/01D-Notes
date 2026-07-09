- [Batch Normalization (BN) (tăng tốc độ huấn luyện và giảm hiện tượng gradient biến mất)](#batch-normalization-bn-tăng-tốc-độ-huấn-luyện-và-giảm-hiện-tượng-gradient-biến-mất)
---
# Batch Normalization (BN) (tăng tốc độ huấn luyện và giảm hiện tượng gradient biến mất)
Tại sao Batch Normalization giúp hội tụ nhanh hơn?
Giả sử bạn có mạng:
Input  ↓Layer 1  ↓Layer 2  ↓Layer 3

Vấn đề khi không có BatchNorm
Khi Layer 1 cập nhật trọng số:
w1 thay đổi
Output của Layer 1 cũng thay đổi:
Layer 1 output:hôm qua: [-1, 2, 3]hôm nay: [50, -20, 100]
Layer 2 đang học dựa trên phân phối cũ:
[-1, 2, 3]
nhưng giờ phải học lại với:
[50, -20, 100]
Layer 2 bị "sốc dữ liệu".
Sau đó Layer 3 cũng bị ảnh hưởng.
Toàn bộ mạng cứ phải thích nghi lại liên tục.

BatchNorm xử lý thế nào?
Sau mỗi layer:
Layer Output      ↓BatchNorm      ↓Activation
BatchNorm ép output về dạng ổn định:
Mean ≈ 0Std ≈ 1
Ví dụ:
Trước:
[100, 120, 90, 130]
Sau BatchNorm:
[-0.7, 0.4, -1.2, 1.5]
Layer sau luôn nhận dữ liệu cùng scale.

Kết quả
Gradient ổn định hơn:
Learning rate có thể lớn hơn
Ít bị:
Exploding GradientVanishing Gradient
Nên:
Epoch ít hơnHội tụ nhanh hơn

2. BatchNorm thực sự chuẩn hóa cái gì?
Giả sử batch size = 4
Feature có 3 chiều:
x1  x2  x31   5   82   6   73   7   64   8   5
BatchNorm nhìn theo từng cột:
x1: [1,2,3,4]x2: [5,6,7,8]x3: [8,7,6,5]
Nó tính:
mean(x1)std(x1)mean(x2)std(x2)mean(x3)std(x3)
rồi normalize từng cột.

Hình dung
Batch↓4 samplesS1S2S3S4
BatchNorm chuẩn hóa:
THEO CHIỀU BATCH↑↓

3. LayerNorm là gì?
LayerNorm không nhìn theo batch.
Nó nhìn từng sample riêng lẻ.
Ví dụ:
Sample:[1, 5, 8]
Tính:
mean = (1+5+8)/3std = ...
rồi normalize chính sample đó.

Hình dung
[1, 5, 8] ↑  ↑  ↑
LayerNorm chuẩn hóa:
THEO CHIỀU FEATURE←────────→

So sánh trực quan
Input:
Sample1: [1,5,8]Sample2: [2,6,7]Sample3: [3,7,6]Sample4: [4,8,5]
BatchNorm
Nhìn theo cột:
1 2 3 4↑feature 15 6 7 8↑feature 28 7 6 5↑feature 3
Normalize từng feature trên toàn batch.

LayerNorm
Nhìn theo hàng:
[1,5,8] ↑ ↑ ↑[2,6,7] ↑ ↑ ↑
Normalize từng sample.

Tại sao Transformer dùng LayerNorm?
Transformer thường xử lý:
1 câu1 document1 token stream
Batch size có thể:
124
rất nhỏ hoặc thay đổi liên tục.
Nếu dùng BatchNorm:
Mean batch không ổn định
=> train khó.
LayerNorm không phụ thuộc batch:
1 sample vẫn chạy tốt1000 sample vẫn chạy tốt
Nên GPT, Gemini, Claude đều dùng:


LayerNorm


hoặc RMSNorm (phiên bản đơn giản hơn)



Mẹo nhớ 5 giây
BatchNorm
Chuẩn hóa theo featurequa nhiều sample trong batch
Nhìn dọc:
↓↓↓

LayerNorm
Chuẩn hóa theo featurebên trong 1 sample
Nhìn ngang:
← → ← →

Bảng nhớ nhanh:
BatchNormLayerNormChuẩn hóa theoBatchSampleTính mean/std từNhiều mẫuMột mẫuPhụ thuộc batch sizeCóKhôngCNNRất phổ biếnÍtTransformerHiếmChuẩn hiện nayGPT/Gemini/Claude❌✅
Một câu cực ngắn:

BatchNorm = "so sánh một feature giữa nhiều mẫu".
LayerNorm = "so sánh các feature bên trong một mẫu".
