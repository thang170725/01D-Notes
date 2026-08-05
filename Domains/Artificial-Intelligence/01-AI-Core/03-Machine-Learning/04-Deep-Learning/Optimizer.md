- [Batch Normalization (BatchNorm) (tăng tốc độ huấn luyện và giảm hiện tượng gradient biến mất)](#batch-normalization-batchnorm-tăng-tốc-độ-huấn-luyện-và-giảm-hiện-tượng-gradient-biến-mất)
- [LayerNorm](#layernorm)
---
# Batch Normalization (BatchNorm) (tăng tốc độ huấn luyện và giảm hiện tượng gradient biến mất)
```bash
Không có BatchNorm: 
    mỗi lần cập nhật ở các layer trước có thể làm đầu vào của các layer sau thay đổi đáng kể, khiến quá trình tối ưu trở nên kém ổn định và hội tụ chậm hơn.

Có BatchNorm: 
    đầu vào của mỗi layer được giữ ở một phân phối ổn định hơn, nên các layer không phải liên tục thích nghi với những thay đổi lớn, giúp huấn luyện nhanh và ổn định hơn.

Tác dụng:
    - Làm gradient ổn định hơn.
    - Cho phép dùng learning rate lớn hơn mà vẫn hội tụ.
    - Làm bề mặt tối ưu (loss landscape) "mượt" hơn, giúp Gradient Descent dễ tìm điểm tối ưu.

Có thể hình dung bằng ví dụ lái xe
    Giả sử bạn đang học lái xe.

    - Nếu hôm nay vô lăng quay 1 vòng để rẽ 30°.
    - Ngày mai tự nhiên phải quay 5 vòng mới rẽ 30°.
    - Ngày kia chỉ cần quay 1/10 vòng đã rẽ 30°.
    => Bạn vẫn có thể học, nhưng sẽ rất khó vì "quy luật đầu vào" thay đổi liên tục.
=> BatchNorm giống như đảm bảo rằng vô lăng luôn có cảm giác lái gần giống nhau. Bạn vẫn phải học lái, nhưng môi trường học ổn định hơn nên tiến bộ nhanh hơn.
```
**Tại sao Batch Normalization giúp hội tụ nhanh hơn?**
```bash
Ví dụ có một mạng:
    Input
      ↓
    Layer 1
      ↓
    Layer 2
      ↓
    Output

Ban đầu Layer 1 tạo ra: [-1, 2, 3]
    Layer 2 học dần dần dựa trên kiểu dữ liệu này.

Sau một bước Gradient Descent
    Giả sử Layer 1 chỉ thay đổi một chút:
        [-1, 2, 3]
            ↓
        [-0.9, 2.1, 2.8]
    => Điều này hoàn toàn bình thường. Layer 2 gần như không bị ảnh hưởng.

Nhưng nếu thay đổi quá mạnh
    Giả sử do learning rate lớn hoặc gradient lớn:
        [-1, 2, 3]
            ↓
        [80, -150, 60]

    => Bây giờ Layer 2 gặp vấn đề. 
        vì layer 1 thay đổi 1 thì layer 2 có thể thay đổi 10 bởi sự nhân chia phức tạp của mạng neural.

BatchNorm làm gì?
    Nó chỉ nói: "Dù Layer 1 tạo ra gì đi nữa, trước khi đưa sang Layer 2, mình sẽ chuẩn hóa nó."

    Ví dụ Layer 1 sinh ra:
        [50,-20,100]

        BatchNorm biến thành gần giống:
            [-0.3, 0.8, 1.2]

        Lần sau Layer 1 sinh:
            [-300,700,-50]

        BatchNorm lại biến thành:
            [-0.5, 0.9, 1.1]
=> Giá trị gốc thay đổi rất nhiều, nhưng phân phối sau BatchNorm vẫn khá ổn định.
```
# LayerNorm
```bash
LayerNorm không nhìn theo batch. Nó nhìn từng sample riêng lẻ.

Mẹo nhớ 5 giây
    BatchNorm: Chuẩn hóa theo featurequa nhiều sample trong batch
        Nhìn dọc: ↓↓↓

    LayerNorm: Chuẩn hóa theo featurebên trong 1 sample
        Nhìn ngang: ← → ← →

    BatchNorm = "so sánh một feature giữa nhiều mẫu".
    LayerNorm = "so sánh các feature bên trong một mẫu".
```
**Tại sao Transformer dùng LayerNorm?**
```bash
Transformer thường xử lý:
    - 1 câu
    - 1 document
    - 1 token stream

Nếu dùng BatchNorm:
    Mean batch không ổn định => train khó.

LayerNorm không phụ thuộc batch:
    - 1 sample vẫn chạy tốt
    - 1000 sample vẫn chạy tốt

Nên GPT, Gemini, Claude đều dùng:
    - LayerNorm
    - RMSNorm (phiên bản đơn giản hơn)
```