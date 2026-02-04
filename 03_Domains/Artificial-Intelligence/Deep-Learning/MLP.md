Bài tập
Demo cách hoạt động của MLP
Đề bài: Cho input là [1,2,3,4,5] và mạng nơ ron 2 lớp 3x2. Demo cách hoạt động của mạng nơ ron này
    1. Khởi tạo tham số ban đầu:
       w11 = [0.1, 0.2, 0.3, 0.4, 0.5], b11 = 0.01
       w12 = [0.11, 0.22, 0.33, 0.44, 0.55], b12 = 0.01
       w13 = [0.15, 0.25, 0.35, 0.45, 0.55], b13 = 0.01
       w21 = [0.1, 0.2, 0.3], b21 = 0.01
       w22 = [0.05, 0.15, 0.2], b21 = 0.01
    2. Tíng giá trị z của mỗi nơ ron:
       z11 = 1x0.1 + 2x0.2 + 3x0.3 + 4x0.4 + 5.0.5 + 0.01 = 5.51
       z12 = 6
       z13 = 6.4
    3. Áp dụng hàm kích hoạt ReLU cho layer 1:
       h11 = 5.51
       h12 = 6
       h13 = 6.4
    4. Tính giá trị z cho mỗi nơ ron ở layer 2:
       z21 = 0.1x5.51 + 0.2x6 + 0.3x6.4 = 3.67
       z22 = 2.58
    5. Áp dụng softmax cho layer 2: softmax = [0.748, 0.252]
    6. Tính độ mất mát (loss) bằng Categorical Cross-Entropy với nhãn thật là [1,0]:
       L = -(1.log(0.748) + 0.log(252)) = 0.126
    7. Backpropagation:
       dL/dz2k = d2k = pk – yk
       …
    8. Cập nhật lại trọng số và bias
       w := w -alpha*&w
       b := b – alpha*&b
Xây dựng mạng neural 1 lớp 2 nơ ron