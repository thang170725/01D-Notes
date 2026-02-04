Deep Learning
Batch Normalization (BN)
Là một kỹ thuật giúp tăng tốc độ huấn luyện và giảm hiện tượng gradient biến mất, bằng cách chuẩn hóa (normalize) đầu ra của mỗi layer (thường là sau Conv2D hoăc Dense).
MLP (Multi-layer Perceptron)
    • Là một mạng nơ-ron nhân tạo gồm nhiều lớp tuyến tính kết hợp với các hàm kích hoạt phi tuyến.
Ứng dụng:
    • Phần loại hình ảnh, văn bản.
    • Dự đoán giá trị (hồi quy).
    • Dự đoán chuỗi thời gian.
Cấu trúc cơ bản:
    1. Input layers: Nhận dữ liệu đầu vào dạng vector.
    2. Hidden layers (1 hoặc nhiều): Mỗi lớp gồm nhiều nơ ron, mỗi neuron tính tổng có trọng số của đầu vào rồi áp dụng activation function như ReLU, sigmoid, tanh …
    3. Output layer: Trả về kết quả cuối cừng, có thể là phần loại, hồi quy, …
Cơ chế hoạt động:
    • MLP, còn được gọi là mạng truyền thẳng (Feedforward Network), được cấu tạo từ các lớp (layer): Lớp đầu vào, một hoặc nhiều lớp ẩn, và lớp đầu ra.
    • 1. Phép nhân Ma trận (Matrix Multiplication):
        ◦ Đây là cơ chế cốt lõi để tính toán đầu ra của một nơ-ron trong lớp tiếp theo.
        ◦ Đối với mỗi nơ-ron trong lớp ẩn, đầu vào của nó là tổng có trọng số của đầu ra từ tất cả các nơ-ron trong lớp trước.
        ◦ Công thức tổng quát cho tính toán tuyến tính (linear combination) trong một lớp là: Z=XW+B
            ▪ X: Ma trận đầu vào từ lớp trước (hoặc lớp đầu vào).
            ▪ W: Ma trận trọng số (Weights) của lớp hiện tại. Đây là các tham số mà mô hình học được.
            ▪ B: Vector độ lệch (Bias) của lớp hiện tại.
            ▪ Z: Đầu ra tuyến tính.
    • 2. Hàm Kích Hoạt Phi Tuyến tính (Non-linear Activation Function)
        ◦ Sau khi tính toán tuyến tính (Z), kết quả này sẽ được truyền qua một hàm kích hoạt (ví dụ: Sigmoid, ReLU, Tanh).
        ◦ Công thức: A=f(Z)
            ▪ A: Đầu ra đã được kích hoạt (activation), đây chính là đầu vào cho lớp tiếp theo.
            ▪ f: Hàm kích hoạt phi tuyến tính.
Tầm quan trọng: Cơ chế này là quan trọng nhất vì nếu không có hàm kích hoạt phi tuyến tính, dù MLP có bao nhiêu lớp đi chăng nữa, nó vẫn chỉ có thể mô hình hóa các mối quan hệ tuyến tính (giống như hồi quy tuyến tính). Khả năng học các mối quan hệ phức tạp và phi tuyến tính của dữ liệu (ví dụ: phân loại hình ảnh, dịch máy) đến từ việc sử dụng các hàm kích hoạt này.
