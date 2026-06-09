- [Giải tích](#giải-tích)
  - [Đạo hàm](#đạo-hàm)
  - [Gradient (gom tất cả đạo hàm thành một mũi tên)](#gradient-gom-tất-cả-đạo-hàm-thành-một-mũi-tên)
  - [Gradient descent](#gradient-descent)
- [Xác suất thống kê](#xác-suất-thống-kê)
  - [Định lý Bayes (cập nhật xác suất khi có thêm thông tin mới)](#định-lý-bayes-cập-nhật-xác-suất-khi-có-thêm-thông-tin-mới)
  - [Phân phối xác suất](#phân-phối-xác-suất)
    - [Normal \& Gaussian](#normal--gaussian)
    - [Bernoulli](#bernoulli)
    - [Binomial](#binomial)
    - [Central Limit Theorem (CLT) (Định lý giới hạn trung tâm)](#central-limit-theorem-clt-định-lý-giới-hạn-trung-tâm)
- [Đại số tuyến tính](#đại-số-tuyến-tính)
  - [Vector (một trạng thái, vị trí trong không gian)](#vector-một-trạng-thái-vị-trí-trong-không-gian)
    - [Tính vô hướng](#tính-vô-hướng)
  - [Norm 1 (Chuẩn 1)](#norm-1-chuẩn-1)
  - [Norm 2 (Chuẩn 2)](#norm-2-chuẩn-2)
  - [Ma trận (một cỗ máy biến đổi không gian)](#ma-trận-một-cỗ-máy-biến-đổi-không-gian)
    - [Phép nhân ma trận (ghép các phép biến đổi)](#phép-nhân-ma-trận-ghép-các-phép-biến-đổi)
    - [Ma trận chuyển vị (Transpose)](#ma-trận-chuyển-vị-transpose)
    - [Ma trận nghịch đảo](#ma-trận-nghịch-đảo)
    - [Định thức của ma trận (det)](#định-thức-của-ma-trận-det)
  - [Eigenvalue \& Eigenvector (những hướng đặc biệt của vũ trụ)](#eigenvalue--eigenvector-những-hướng-đặc-biệt-của-vũ-trụ)
  - [SVD (giải phẫu mọi phép biến đổi)](#svd-giải-phẫu-mọi-phép-biến-đổi)
  - [Ma trận Gram](#ma-trận-gram)
  - [eigenvector \& eigenvalue](#eigenvector--eigenvalue)
    - [demo eigenvalue \& eigenvector](#demo-eigenvalue--eigenvector)
    - [Trích xuất đặc trựng ảnh 100x100 bằng eigen](#trích-xuất-đặc-trựng-ảnh-100x100-bằng-eigen)
---
# Giải tích
## Đạo hàm
```bash
- Đạo hàm là “tốc độ thay đổi” của một đại lượng.
- Đạo hàm cho biết độ dốc và hướng thay đổi của một hàm số. Gradient Descent dùng thông tin này để biết phải đi theo hướng nào để làm cho giá trị hàm nhỏ nhất
- Tối ưu hóa: Tìm điểm nhỏ nhất, lớn nhất trong hàm (mất mát trong ML).
- Kinh tế: Tối đa hóa lợi nhuận, tối thiểu hóa chi phí.
- Vật lý: Mối liên hệ giữa vị trí - vận tốc - gia tốc.
- ML/DL: Sử dụng tính toán hàm mất mát (gradient descent).Nếu không có đạo hàm → máy không biết “học” thế nào để tốt hơn.
- Game: Mô phỏng chuyển động, ánh sáng, âm thanh.
- Sinh học/Hóa học: Mô hình hóa phản ứng, lan truyền, tăng trưởng, …
```
**Đạo hàm riêng là gì?**
```bash
Khi hàm phụ thuộc vào nhiều biến, ví dụ: f(x,y)=x^2+y^2

Ta có thể hỏi:
    1. Nếu chỉ thay đổi x và giữ y cố định thì hàm đổi thế nào?
    2. Nếu chỉ thay đổi y và giữ x cố định thì hàm đổi thế nào?

=> Đó chính là đạo hàm riêng.
```
**Ex**
```bash
f(x,y)=x^2+y^2

Tại điểm (x,y)=(3,4):
    - df/dx = 6
    - df/dy = 8
Điều này nghĩa là: tăng x một chút làm hàm tăng khoảng 6 lần mức thay đổi; tăng y một chút làm hàm tăng khoảng 8 lần mức thay đổi.
```
## Gradient (gom tất cả đạo hàm thành một mũi tên)
```bash
∇L = [dL/dw1, dL/dw2, ..., dL/dwn]
    - Nó là một vector mũi tên cho biết:
        + Hướng tăng nhanh nhất của loss. Gradient chỉ “đi hướng này thì loss tăng mạnh nhất”.
    - Mức độ dốc theo từng tham số.
        + Thành phần nào lớn → tham số đó đang làm loss nhạy hơn.
    - Mẹo nhớ 5 giây
        + Gradient = mũi tên chỉ lên dốc. Muốn giảm loss thì đừng đi theo gradient. Hãy đi ngược lại.
```
## Gradient descent
**Formula**
```bash
w_t+1 = w_t - lambda*lr
    - Đứng tại bộ tham số hiện tại, w_t
	​- Tính gradient ∇L(wt) (độ dốc và hướng lên dốc).
    - Đi ngược lại nên có dấu −.
    - Bước một đoạn nhỏ. η (learning rate).
    - Lặp lại cho đến khi loss không giảm đáng kể nữa.
```
# Xác suất thống kê
## Định lý Bayes (cập nhật xác suất khi có thêm thông tin mới)
```bash
- Nói đơn giản: “Ban đầu mình nghĩ khả năng xảy ra là bao nhiêu, rồi sau khi thấy bằng chứng mới thì nên tin lại như thế nào?”
- Ý nghĩa trực quan
    + Bayes giống như: Niềm tin cũ + bằng chứng mới = niềm tin mới
    + Ví dụ:
        - trời nhiều mây → nghĩ sắp mưa
        - nghe sấm → tin mưa hơn nữa
- Ứng dụng cực phổ biến
    + AI & Machine Learning
        - spam email
        - nhận diện ảnh
        - chatbot
        - recommendation
    + Y học
        - chẩn đoán bệnh
        - đánh giá kết quả xét nghiệm
        - Tài chính
        - dự đoán rủi ro
        - gian lận giao dịch
        - Điều tra
        - suy luận nghi phạm từ chứng cứ
- Bayes trong AI. Một thuật toán nổi tiếng: Naive Bayes Dùng xác suất Bayes để:
    + phân loại email spam
    + phân tích cảm xúc
    + lọc văn bản
    + “Naive” vì giả sử các đặc trưng độc lập với nhau.
```
**Formula**
```bash
P(A|B) = (P(B|A).P(A))/P(B)

- Input:
    + P(A)  : xác suất ban đầu của A (prior)
    + P(B|A): xác suất thấy B nếu A đúng
    + P(B)  : xác suất xảy ra B
- Output:
    + P(A|B): xác suất A đúng sau khi đã biết B xảy ra
```
**Ex1: Hộp bi**
```bash
Có 2 hộp:
    - Hộp A: 9 đỏ, 1 xanh
    - Hộp B: 1 đỏ, 9 xanh
Chọn ngẫu nhiên một hộp. Xác suất ban đầu:
    - P(A) = 50%
    - P(B) = 50%
Đây gọi là prior probability (niềm tin ban đầu). Bây giờ bạn rút được một viên bi đỏ.
Câu hỏi: Khả năng bạn đang cầm hộp A là bao nhiêu?
Trước khi nhìn màu bi:
    - A: 50%
    - B: 50%
Sau khi thấy bi đỏ:
    - A có vẻ hợp lý hơn vì:
        + P(đỏ | A) = 90%
        + P(đỏ | B) = 10%
Nói cách khác:
    + Nếu hộp A là thật thì việc nhìn thấy bi đỏ rất bình thường.
    + Nếu hộp B là thật thì việc nhìn thấy bi đỏ khá bất thường.
    + Do đó ta tăng niềm tin vào A.
```
**Ex: Ví dụ Bayes trong xét nghiệm bệnh**
```bash
- Giả sử:
    + 1% dân số bị bệnh
    + Test đúng nếu có bệnh: 99%
    + Test nhầm dương tính khi không bệnh: 5%
- Một người test dương tính. Hỏi: người đó thực sự bị bệnh bao nhiêu %?
```
```bash
Bước 1: Đặt biến
    - A = "có bệnh"
    - B = "test dương tính"
    - Ta có:
        + P(A) = 0.01
        + P(B|A) = 0.99
        + P(B|¬A) = 0.05
Bước 2: Tính xác suất test ra dương tính
    - P(B) = P(B|A).P(A) + P(B∣¬A).P(¬A) = 0.99*0.0.1 + 0.05*0.99 = 0.0594
Bước 3: Áp dụng Bayes
    - P(A|B) = (0.99*0.01)/0.0594 = 0.1667
    => dùng test dương tính, xác suất thực sự bị bệnh chỉ khoảng 16.7%
```
## Phân phối xác suất
### Normal & Gaussian
```bash
- Đây là phân phối hình “chuông úp”, dữ liệu tập trung quanh giá trị trung bình.
- Dùng khi nào?
    + Khi dữ liệu tự nhiên dao động quanh mức trung bình:
        - chiều cao con người
        - điểm thi
        - nhiệt độ
        - lỗi đo lường
    + Ví dụ: Chiều cao nam sinh
        - trung bình: 170 cm
        - đa số nằm khoảng 165–175 cm
        - rất ít người 150 cm hoặc 195 cm
        => tạo thành đường cong chuông.
- Ý nghĩa
    + gần trung bình → xuất hiện nhiều
    + càng xa trung bình → càng hiếm
```
**Formula**
```bash
y = e**(-x**2)
```
### Bernoulli
```bash
- Mô hình cho 1 lần thử chỉ có 2 kết quả:
    + thành công / thất bại
    + đúng / sai
    + có / không
- Ví dụ
    + Tung đồng xu 1 lần:
        - ngửa = 1
        - sấp = 0
    + Nếu xác suất ngửa là 0.5:
        - P(X=1)=0.5
        - P(X=0)=0.5
- Dùng khi nào?
    + Khi chỉ có:
        - 1 lần thử
        - 2 kết quả
```
### Binomial
```bash
- Là mở rộng của Bernoulli:
    + nhiều lần thử độc lập
    + đếm số lần thành công
- Ví dụ: Tung đồng xu 10 lần. Hỏi: Xác suất ra đúng 7 mặt ngửa? Đây là Binomial.
- Điều kiện
    + số lần thử cố định: n
    + mỗi lần chỉ có 2 kết quả
    + xác suất mỗi lần giống nhau
```
### Central Limit Theorem (CLT) (Định lý giới hạn trung tâm)
```bash
- Một trong những định lý quan trọng nhất của thống kê.
- Ý tưởng cực ngắn:
    + Lấy trung bình của rất nhiều mẫu → kết quả sẽ gần phân phối chuẩn.
    + Cho dù dữ liệu gốc không chuẩn.
- Ví dụ dễ hiểu
    + Giả sử:
        - xúc xắc không hề phân phối chuẩn
        - số ra từ 1→6 là đồng đều
    + Bây giờ:
        - Tung xúc xắc 30 lần
        - Tính trung bình
        - Lặp lại 10,000 lần
    👉 Histogram của các giá trị trung bình sẽ thành hình chuông (Normal).
- Vì sao quan trọng?
    + CLT giải thích vì sao:
        - thống kê thường dùng phân phối chuẩn
        - trung bình mẫu rất hữu ích
        - nhiều mô hình ML/statistics hoạt động tốt
```
# Đại số tuyến tính
## Vector (một trạng thái, vị trí trong không gian)
```bash
- “một mũi tên trong không gian”
- Trực giác vật lý
    + Vector là:
        - một hướng
        - và một độ lớn
- Ví dụ vật lý:
    + vận tốc của gió
    + lực tác dụng lên vật
    + hướng chuyển động
    + điện trường
```
**Ex**
```bash
- Một vector không chỉ là dãy số. v = [3 2]
- nghĩa là:
    + đi sang phải 3
    + đi lên 2
=> Tức là một mũi tên trong không gian 2D.
```
### Tính vô hướng
**Fomula**
```bash
xy = x1.y1 + ... + xn.yn hoặc <x, y> = x**T * y

- Output: 1 số
```
**Fomula**
```bash
x.y = ||x||.||y||.cos(x,y) # với ||...|| được xác định là chuẩn 2
```
## Norm 1 (Chuẩn 1)
**Ex**
```bash
||x||1 = |x1| + |x2| + ... + |xn|
```
**Tính chất**
```bash
1. ||u|| >= 0
2. ||au|| = |a|.||u||
3. ||u+v|| <= ||u|| + ||v||
4. ||u|| = 0 only when u = 0
```
## Norm 2 (Chuẩn 2)
**Ex**
```bash
x = (1,2) y = (3,6)

||x-y||2 = sqrt((x1-y1)**2 + (x2-y2)**2) = sqrt(20)
cos(x,y) = x.y/(||x||.||y||) =  15/(sqrt(5)+sqrt(45)) = 1
=> đây là 2 vector cùng hướng y dài hơn 3 lần so với x
```
## Ma trận (một cỗ máy biến đổi không gian)
```bash
- Nhiều người nghĩ ma trận chỉ là “bảng số”. Không.
- Bản chất thật:
    + Ma trận là một phép biến đổi tuyến tính.
    + Nó nhận một vector đầu vào và biến đổi nó.
```
**Ex: vật lý**
```bash
Giả sử có vector: v = [1 1] và ma trận: A = [[2 0] [0 1]]
Khi nhân: A.v_vector ta được: [2 1]
Điều gì vừa xảy ra?
    - Không gian bị:
    - kéo dãn theo trục x gấp đôi
    - trục y giữ nguyên
Tức là:
    - ma trận đang “bóp méo” không gian.
    - Góc nhìn vật lý.
        + Ma trận có thể biểu diễn:
            - xoay
            - kéo dãn
            - phản xạ
            - shear (nghiêng)
            - biến đổi tọa độ
            - tiến hóa trạng thái hệ vật lý
```
### Phép nhân ma trận (ghép các phép biến đổi)
**Ex1**
```bash
- Nếu:
    + ma trận A = xoay
    + ma trận B = kéo dãn
- thì:
    + AB nghĩa là:
        - làm B trước, rồi làm A sau.
- Trong AI Mỗi layer neural network là: Wx+b
    + x: vector trạng thái
    + W: ma trận biến đổi
    + Deep learning thực chất là: chuỗi các phép biến đổi không gian rất phức tạp.
```
**Ex2: Vật lý trực quan**
```bash
- Tưởng tượng: bạn kéo tấm cao su rồi xoay nó
- khác với: xoay trước rồi kéo
- Nên: AB khác BA
- Đây là lý do phép nhân ma trận không giao hoán.
```
### Ma trận chuyển vị (Transpose)
```bash
- A**T = đổi hàng ↔ cột.
- Transpose mô tả: “phép biến đổi ngược góc nhìn”.
- Trực giác rất quan trọng"
    + Ma trận thường biến đổi vector: A:input→output
    + Transpose đổi vai trò: từ “ảnh hưởng theo hàng” sang “ảnh hưởng theo cột”
- Trong vật lý
    + Transpose liên quan tới:
        - bảo toàn năng lượng
        - đối xứng
        - gradient
        - chiếu trực giao
- Ý nghĩa hình học
    + Nếu ma trận là phép biến đổi không gian, thì transpose là: phép biến đổi nhìn từ hệ tọa độ đối ngẫu (dual space).
- Trực giác AI
    + Trong backpropagation: W**T xuất hiện vì: gradient phải “đi ngược” phép biến đổi ban đầu.
```
### Ma trận nghịch đảo
**Trường hợp ma trận 2×2**
```bash
Nếu A = [[a, c], [b, d]] (2x2)
	​- det(A) = ad−bc
=> A^−1 = (1/ad−bc)*[[d, -b], [-c a]] # với điều kiện ad−bc != 0

Ví dụ:
	A = [[1,2],[3,4]]
	=> A**−1 = (1/-2)*[[4, -2], [-3, 1]]
```
**Thực tế khi tính tay**
```bash
Đối với ma trận 3×3 trở lên, người ta thường dùng:
	- Khử Gauss–Jordan trên [A∣I].
	- Phân tích LU.
	- Các thư viện số học (NumPy, Eigen, MATLAB, v.v.).
Ít khi tính trực tiếp bằng công thức A
```
### Định thức của ma trận (det)
## Eigenvalue & Eigenvector (những hướng đặc biệt của vũ trụ)
```bash
- Thông thường: ma trận sẽ xoay, kéo, bóp méo vector NHƯNG có vài hướng đặc biệt mà: sau biến đổi, hướng không đổi. Chỉ bị kéo dài hoặc co lại. Đó là eigenvector.

Ý nghĩa vật lý
	Eigenvector là:
		“trục tự nhiên” của phép biến đổi.
	Eigenvalue là:
		mức độ kéo dãn theo trục đó.
```
**Formula**
```bash
A.v_vector = λ.v_vertor

- v_vertor: eigenvector
- λ: eigenvalue
```
**Ex: Ví dụ vật lý thực sự**
```bash
Dao động cơ học
	Khi cây cầu rung:
		- có những mode rung tự nhiên => Đó là eigenvectors.
		- Tần số rung tương ứng là eigenvalues.

Trong lượng tử
	Toán tử Hamiltonian:
		- eigenvector = trạng thái lượng tử ổn định
		- eigenvalue = mức năng lượng

Trong AI / PCA
	- Eigenvectors cho biết: hướng dữ liệu biến thiên mạnh nhất.

Trực giác hình học
	Một hình tròn bị biến thành ellipse.
	Các trục chính của ellipse: chính là eigenvectors.
```
**Ex**
```bash
A = [[1, 2], [4, 3]]

x = [1,2], lamda=5, lamda=-1
```
## SVD (giải phẫu mọi phép biến đổi)
```bash
- Đây là một trong những ý tưởng đẹp nhất của đại số tuyến tính.
- Ý tưởng lớn MỌI ma trận đều có thể phân tích thành:
    + A = UΣV**T
- Ý nghĩa vật lý cực đẹp SVD nói rằng:
    + mọi phép biến đổi phức tạp thực chất chỉ là:
        - xoay
        - kéo dãn
        - xoay tiếp
Cụ thể
V
T

Xoay không gian đầu vào.

Σ

Kéo dãn theo các trục độc lập.

Các giá trị trên đường chéo:

gọi là singular values.
U

Xoay không gian đầu ra.

Trực giác cực mạnh

SVD giống như:

tìm hệ trục “tự nhiên nhất”
để mô tả phép biến đổi.

Ví dụ vật lý

Tưởng tượng:

bạn cầm một cục đất sét
xoay nó
bóp theo vài hướng chính
rồi xoay lại

Đó chính là SVD.

Tại sao SVD quan trọng khủng khiếp?

Vì nó:

nén dữ liệu
lọc nhiễu
tìm cấu trúc ẩn
PCA
recommender systems
latent semantics
diffusion models
LLM compression

đều dựa trên nó.

Trực giác sâu nhất
Eigen decomposition

Tìm:

“các hướng bất biến”.

SVD

Tìm:

“cách đơn giản nhất để mô tả mọi biến đổi”.
```
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
