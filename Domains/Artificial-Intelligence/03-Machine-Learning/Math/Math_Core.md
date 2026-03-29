- [Phương sai](#phương-sai)
- [Độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu](#độ-lệch-chuẩn-tổng-thể-và-độ-lệch-chuẩn-mẫu)
- [Đại số tuyến tính](#đại-số-tuyến-tính)
  - [Ma trận Gram](#ma-trận-gram)
  - [eigenvector \& eigenvalue](#eigenvector--eigenvalue)
    - [demo eigenvalue \& eigenvector](#demo-eigenvalue--eigenvector)
    - [Trích xuất đặc trựng ảnh 100x100 bằng eigen](#trích-xuất-đặc-trựng-ảnh-100x100-bằng-eigen)
---
# Phương sai
```bash
Phương sai là một số đo cho biết mức độ phân tán của các giá trị trong tập dữ liệu so với giá trị trung bình của tập dữ liệu đó. Phương sai cho biết các giá trị trong tập dữ liệu “lan rộng” ra sao xung quanh giá trị trung bình.
Phương sai càng lớn thì giá trị trong tập dữ liệu càng phân tán xa so với giá trị trung bình và ngược lại.
```
# Độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu 
**Ex: 5 số 12,34,45,70,86**
```bash
1. Tính trung bình cộng: (12 + 34 + 45 + 70 + 86) / 5 = 49.4 
2. 
    Tính phương sai mẫu: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / (5-1) = 854.8 
    Tính phương sai tổng thể: ((12-49.4)**2 + (34-49.4)**2 + (45-49.4)**2 + …) / 5 = 683.84  
3. 
    Tính độ lệch chuẩn của phương sai mẫu: np.sqrt(854.8)= 29.23696291
    Tính độ lệch chuẩn của phương sai tổng thể: np.sqrt(683.84) = 26.15 
```
# Đại số tuyến tính
## Ma trận Gram
**Ex**
```bash
Giả sử bạn có 3 loại đặc trưng (features):
    + F1 = “màu đỏ”
    + F2 = “cạnh ngang”
    + F3 = “vùng sáng”
Và trong một ảnh, bạn thống kê xem mỗi feature xuất hiện bao nhiêu ở mỗi vị trí.
Ta có ma trận: 𝐹 = [[1, 2, 0, 1], [0, 1, 1, 0], [2, 2, 1, 1]]
    + 3 dòng = 3 feature (F1, F2, F3)
    + 4 cột = 4 vị trí trong ảnh
Tính Gram ta được: 𝐺 = [[6, 2, 7], [2, 2, 3], [7, 3, 10]]
    + G(1,1) = 6 → tổng năng lượng của feature 1
    + G(1,2) = 2 → feature 1 và feature 2 có hay xuất hiện cùng nhau không?
    + G(1,3) = 7 → feature 1 và feature 3 xuất hiện cùng nhau khá nhiều
Gram không quan tâm:
    + feature xuất hiện ở vị trí nào
Nó chỉ quan tâm:
    + Feature A và B có hay đi chung không?
```
## eigenvector & eigenvalue
```bash
- eigenvector   : Hướng đặc biệt không bị đổi hướng khi qua ma trận
- eiganvalue    : mức độ phóng to thu nhỏ theo hướng đó.
    + eigenvalue > 1: nổ (độ dài tăng vô hạn)
    + eigenvalue < 1: triệt (về 0)
    + eigenvalue = 1: giữ biên / dạo động / nghiên về một hướng
```
**Dùng để làm gì**
```bash
1. tìm ra cái “quan trọng nhất / ổn định nhất” trong một hệ phức tạp.
```
### demo eigenvalue & eigenvector
```python
import numpy as np

A = np.array([[0.9, 0.4],
              [0, 0.9]])

# Tính eigen
eigenvalues, eigenvectors = np.linalg.eig(A)

print("Eigenvalues:", eigenvalues)
print("Eigenvectors:\n", eigenvectors)

# Kiểm tra Av = λv với eigen đầu tiên
v = eigenvectors[:, 0]
lam = eigenvalues[0]

print("A @ v =", A @ v)
print("λ * v =", lam * v)

# Eigenvalues: [0.9 0.9] - Ma trận có 1 eigenvalue = 0.9 với bội đại số = 2. |λ|=0.9 < 1 -> không nổ -> A**n -> 0
# Eigenvectors:
#  [[ 1.00000000e+00 -1.00000000e+00]
#  [ 0.00000000e+00  4.99600361e-16]]
# A @ v = [0.9 0. ]
# λ * v = [0.9 0. ]
```
### Trích xuất đặc trựng ảnh 100x100 bằng eigen
```python
import matplotlib.pyplot as plt
import numpy as np

import numpy as np
import matplotlib.pyplot as plt

# Tạo ảnh 100x100 giả
np.random.seed(0)
I = np.zeros((100, 100))

# Thêm "mặt mèo" giả
I[30:70, 30:70] = 200          # mặt
I[40:50, 40:50] = 50           # mắt trái
I[40:50, 60:70] = 50           # mắt phải
I += 20 * np.random.randn(100, 100)  # nhiễu

plt.imshow(I, cmap="gray")
plt.title("Input image")
plt.colorbar()
plt.show()

# Ma trận Gram
G = I.T @ I   # (100x100)

# Eigen decomposition
eigenvalues, eigenvectors = np.linalg.eigh(G)

# Sắp xếp eigen giảm dần
idx = np.argsort(eigenvalues)[::-1]
eigenvalues = eigenvalues[idx]
eigenvectors = eigenvectors[:, idx]

plt.plot(eigenvectors[:, 0])
plt.title("Top eigenvector (dominant pattern)")
plt.show()

k = 10  # số đặc trưng muốn lấy

features = []
for i in range(k):
    v = eigenvectors[:, i]
    feature = I @ v      # (100,)
    features.append(feature)

features = np.array(features)
print("Feature shape:", features.shape)
```
# Computer Vision
## Kernel
```bash
- Phần lớn các bộ lọc đều dựa trên khái niệm convolution (tích chập) – tức là áp một ma trận (kernel) lên từng vùng nhỏ của ảnh để tính toán giá trị mới cho pixel trung tâm. 
- Cách áp dụng kernel này có một quy tắc chuẩn:
    + Duyệt từng pixel trong ảnh gốc.
    + Với mỗi pixel, lấy vùng lân cận (theo kích thước kernel), nhân chéo với kernel.
    + Tính tổng và gán giá trị kết quả vào pixel tương ứng trong ảnh mới.
```
## Gaussian Blur
```bash
Dùng kernel theo phân phối Gauss – làm mờ mịn, tự nhiên hơn.
```
## Median Blur
```bash
Lấy giá trị trung vị trong vùng lân cận – khử nhiễu muối tiêu.
```
## Sharpen (làm sắc nét)
```bash
Dùng kernel làm nổi bật cạnh, tăng tương phản cục bộ.
```
## Sobel, Laplacian
```bash
Dùng để phát hiện biên cạnh – áp kernel đạo hàm.
```
Thuật toán ID3 (Iterative Dichotomiser 3)
    • Là thuật toán xây dựng cây quyết định bằng cách chọn thuộc tính “tốt nhất” để chia dữ liệu tại mỗi bước.
    • Thuộc tính “tốt nhất” được chọn dựa trên việc giảm độ hỗn loạn (entropy) nhiều nhất → nghĩa là giúp dữ liệu trở nên “thuần” nhất có thể.
Entropy (độ hỗn loạn):
Cho biết một tập dữ liệu có lẫn lộn hay không. (Khi chia dữ liệu theo thuộc tính A thì độ hỗn loạn mới là bao nhiêu)
Công thức:
Entropy(S) = -[p1.log2(p1) + p2.log2(p2) + … ]
    • pi: phần trăm mẫu thuộc lớp i (ví dụ: [‘no’, ‘no’, ‘yes’, ‘yes’, ‘yes’] thì p_no = 2/5). Nếu tập đã thuần (100% Yes) → entropy = 0 (không hỗn loạn).
    • Nếu chia đều (50% Yes - 50% No) → entropy = 1 (hỗn loạn tối đa).
EntropyA(S) = [(|Sv1| / S) * Entropy(Sv1) + (|Sv2| / S) * Entropy(Sv2) + ...]
    • Chia dữ liệu theo thuộc tính A → thành nhiều nhóm (ví dụ “Weather” → Sunny/Rain/Windy…)
    • Tính entropy của từng nhóm.
    • Lấy trung bình theo trọng số số lượng mẫu.
Information Gain (độ tăng thông tin):
Sự giảm hỗn loạn khi chia theo thuộc tính. Thuộc tính có Information Gain cao nhất → chọn làm node.
Gain(S,A)=Entropy(S)−EntropyA(S)
    • Gain = mức giảm độ hỗn loạn khi chia bằng A.
    • A càng làm tập “thuần” hơn → Gain càng lớn → được chọn.
Bài tập
Demo cây quyết định với thuật toán id3