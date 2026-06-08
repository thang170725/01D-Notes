- [Parameter (tham số mô hình)](#parameter-tham-số-mô-hình)
- [Hyperparameter](#hyperparameter)
- [Phương sai](#phương-sai)
- [Độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu](#độ-lệch-chuẩn-tổng-thể-và-độ-lệch-chuẩn-mẫu)
- [Bias và Variance](#bias-và-variance)
- [Computer Vision](#computer-vision)
  - [Kernel](#kernel)
  - [Gaussian Blur](#gaussian-blur)
  - [Median Blur](#median-blur)
  - [Sharpen (làm sắc nét)](#sharpen-làm-sắc-nét)
  - [Sobel, Laplacian](#sobel-laplacian)
- [clustering (gom cụm)](#clustering-gom-cụm)
- [Tree](#tree)
  - [Bagging (Bootstrap Aggregating)](#bagging-bootstrap-aggregating)
  - [Boosting](#boosting)
  - [Gradient Boosting](#gradient-boosting)
---
# Parameter (tham số mô hình)
```bash
Là những giá trị mà mô hình tự học được từ dữ liệu.

Ví dụ Linear Regression:
    y=w1.x1+w2.x2+b
        - Ở đây:
            + w1, w2
            + b
        => là parameters.

        - Sau khi train:
            + w1 = 2.5
            + w2 = -1.3
            + b = 10
=> Mô hình tự tìm ra các giá trị này.
```
# Hyperparameter
```bash
Là những giá trị do con người đặt trước khi train. Mô hình không tự học chúng.

Ví dụ:
    - learning_rate = 0.001
    - batch_size = 32
    - epochs = 100

Bạn phải quyết định:
    - học nhanh hay chậm
    - batch lớn hay nhỏ
    - train bao lâu
```
**Các hyperparameter cốt lõi**
```bash
1. Learning Rate (quan trọng nhất)
    Ký hiệu thường: η hoặc learning_rate

2. Batch Size
    Ví dụ: 100000 ảnh
    Không thể đưa hết vào RAM.
    Chia thành: batch_size = 32 hoặc batch_size = 64

3. Epochs
    Một epoch: Đi qua toàn bộ dataset 1 lần
    Ví dụ: 10000 ảnh
        Epoch 1: xem hết 10000 ảnh
        Epoch 2: xem lại 10000 ảnh

4. Regularization (L1/L2)
    Dùng để chống overfitting.


5. Number of Trees (Random Forest, XGBoost)
    Ví dụ: n_estimators = 100
        Ít cây - 10 cây
            - train nhanh
            - độ chính xác thấp
            - Nhiều cây
        1000 cây
            - chính xác hơn
            - train chậm hơn

6. Max Depth
    Áp dụng cho cây quyết định.

7. k trong KNN
    k = 3 nghĩa là xem 3 hàng xóm gần nhất.
```
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
# Bias và Variance 
```bash
Là hai khái niệm cực kỳ quan trọng trong Machine Learning. Nếu hiểu được chúng, bạn sẽ hiểu vì sao:
    - Linear Regression đôi khi quá đơn giản.
    - Decision Tree đôi khi overfit.
    - Random Forest lại hiệu quả.
    - Bagging giảm variance.
    - Boosting giảm bias.

Bias = mô hình lệch có hệ thống khỏi đáp án đúng.
Variance = mô hình quá nhạy với dữ liệu train.

Câu thần chú dễ nhớ
    - Bias = mô hình quá ngu vì quá đơn giản
        Không học đủ
        ↓
        Underfitting
    - Variance = mô hình quá thông minh đến mức học thuộc
        Học quá kỹ
        ↓
        Overfitting
    
    Vì thế người ta thường nói:
        - Machine Learning là bài toán cân bằng giữa Bias và Variance.
        - Tăng độ phức tạp mô hình → Bias giảm nhưng Variance tăng.
        - Giảm độ phức tạp mô hình → Variance giảm nhưng Bias tăng.
    => Mục tiêu là tìm điểm cân bằng sao cho mô hình vừa học đủ quy luật của dữ liệu, vừa không học thuộc dữ liệu train.
```
**Ex: bắn cung**
```bash
Hãy tưởng tượng tâm bia là đáp án đúng.
      X
   X  O  X
      X

O = đáp án đúng
X = dự đoán của mô hình

1. Bias là gì?
    Ví dụ:
        X X X
        X X X
        X X X
                  O

        Tất cả mũi tên đều tập trung một chỗ. Nhưng lệch xa tâm.
            Điều này có nghĩa:
                - Mô hình học chưa đủ
                - Nó đang đơn giản hóa vấn đề quá mức.

    Ví dụ dự đoán giá nhà
        Giá thực tế:
            Diện tích	Giá
            50	        2 tỷ
            100	        6 tỷ
            150	        15 tỷ
        Quan hệ thực:    
                  *
                      *
            *
            (Cong mạnh)

        Nhưng bạn dùng Linear Regression: (chỉ là đường thẳng)
            Nó không thể mô tả được dữ liệu. => Sai ở mọi nơi.
        Đây là: High Bias
        
        Dấu hiệu
            - Train: Sai
            - Test: Cũng sai

        Ta gọi là:
            Underfitting

2. Variance là gì?
    Ví dụ:
        Dataset A:     
        50m² -> 2 tỷ
        60m² -> 2.5 tỷ

    Train ra cây:
        Nếu diện tích > 55
        Dataset B:
            Chỉ thay đổi một vài dòng:
            50m² -> 2 tỷ
            61m² -> 2.5 tỷ

    Lại ra cây:
        Nếu diện tích > 58
        Mô hình thay đổi rất mạnh chỉ vì dữ liệu thay đổi chút ít.
        Đó là: High Variance

    Ví dụ bắn cung
        X        X

             O

                  X

         X

        Các mũi tên bay lung tung. Không ổn định.
        => Overfitting chính là High Variance

Ví dụ có dữ liệu:

*
 *
  *
   *
    *

Decision Tree rất sâu:

Nếu tuổi = 31
Nếu tuổi = 32
Nếu tuổi = 33
Nếu tuổi = 34
...

Nó học thuộc dữ liệu.

Train:

99%

Test:

70%

Đây là:

High Variance
Bias vs Variance
High Bias
Train error  = cao
Test error   = cao

Mô hình quá đơn giản.

Ví dụ:

Linear Regression cho dữ liệu phức tạp
Tree quá nông
High Variance
Train error = thấp
Test error  = cao

Mô hình quá phức tạp.

Ví dụ:

Decision Tree cực sâu
Neural Network quá lớn
Minh họa 4 trường hợp
1. Bias thấp, Variance thấp

Lý tưởng

      X
    X O X
      X

Vừa đúng vừa ổn định.

2. Bias cao, Variance thấp
X X X
X X X
X X X


         O

Mọi dự đoán đều giống nhau.

Nhưng sai.

3. Bias thấp, Variance cao
X       X

     O

          X

 X

Trung bình gần đúng.

Nhưng mỗi lần dự đoán lại khác nhau.

4. Bias cao, Variance cao
X


X


      X


                O

Vừa sai vừa không ổn định.

Tệ nhất.
```
**Ex: Dự đoán giá nhà**
```bash
Giả sử bạn có dataset dự đoán giá nhà:
    Diện tích   Giá
    50          2 tỷ
    60          2.5 tỷ
    70          3 tỷ
    80          3.5 tỷ
    ...         ...
Bạn huấn luyện một cây quyết định.

Cây quyết định có nhược điểm:
    - Rất nhạy với dữ liệu train
    - Chỉ cần thay đổi vài dòng dữ liệu:
        + Dataset A => Tree A
        + Dataset B (khác một chút) => Tree B
        Có thể cho ra hai cây hoàn toàn khác nhau.
Ta gọi đây là high variance.
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
# clustering (gom cụm)
**Gom cụm cứng và gom cụm mềm**
```bash
có hai kiểu phân cụm phổ biến:
    1. Gom cụm cứng (Hard Clustering): Mỗi điểm dữ liệu chỉ được thuộc đúng 1 cụm duy nhất.
        Ví dụ bạn có dữ liệu khách hàng:
            | Khách hàng | Cụm    |
            | ---------- | ------ |
            | A          | Nhóm 1 |
            | B          | Nhóm 1 |
            | C          | Nhóm 2 |
            | D          | Nhóm 3 |
        Khách hàng A thuộc nhóm 1 thì không thể thuộc nhóm khác
        
        Ví dụ trực quan. Phân loại động vật:
            - Con mèo → Nhóm Mèo
            - Con chó → Nhóm Chó
        Một con vật chỉ nằm trong một nhóm.

        Thuật toán tiêu biểu
            - K-Means
            - K-Medoids
            - DBSCAN
    
    2. Gom cụm mềm (Soft Clustering)
        Một điểm dữ liệu có thể thuộc nhiều cụm với các mức độ khác nhau.
        
        Ví dụ:
        | Khách hàng | Nhóm 1 | Nhóm 2 |
        | ---------- | ------ | ------ |
        | A          | 80%    | 20%    |
        | B          | 40%    | 60%    |
        A chủ yếu thuộc nhóm 1 nhưng vẫn có nét giống nhóm 2.
    
        Ví dụ trực quan. Giả sử bạn phân loại người theo sở thích:
            - Người A: 
                + Thích bóng đá: 70%
                + Thích game: 30%
            - Người B:
                + Thích bóng đá: 45%
                + Thích game: 55%
        => Rất khó nói họ thuộc hoàn toàn một nhóm nào.

        Hard Clustering. K-Means sẽ nói: x -> Cụm đỏ hoặc x -> Cụm xanh. Không có lựa chọn khác.
        Soft Clustering. Thuật toán có thể nói: x:70% cụm đỏ và 30% cụm xanh
            -> Nghe hợp lý hơn vì nó nằm giữa hai cụm.

        Thuật toán gom cụm mềm nổi tiếng
            - Fuzzy C-Means
            - Gaussian Mixture Model (GMM)

Khi nào dùng cái nào?
    - Hard Clustering. Khi bạn cần quyết định rõ ràng:
        + Phân nhóm khách hàng
        + Phân loại khu vực địa lý
        + Chia người dùng thành các segment
        Ví dụ: Khách hàng này thuộc nhóm VIP hay không? Cần câu trả lời dứt khoát.
    - Soft Clustering. Khi ranh giới không rõ ràng:
        + Phân tích hành vi khách hàng
        + Phân tích văn bản
        + Hệ gợi ý
        + Nhận dạng mẫu
        Ví dụ: Bộ phim này: 60% hành động 30% hài 10% tâm lý. Một bộ phim không nhất thiết chỉ thuộc một thể loại.
```
# Tree
## Bagging (Bootstrap Aggregating) 
```bash
Ý tưởng của Bagging, Thay vì:
    1 Dataset => 1 Tree => Prediction
    Ta làm:
    1 Dataset => Tạo nhiều dataset con => Train nhiều cây => Gộp kết quả

Tóm tắt dễ nhớ. Bagging hoạt động theo 3 bước:
    1. Bootstrap # Tạo nhiều dataset con bằng lấy mẫu có hoàn lại
    2. Train     # Huấn luyện một model trên mỗi dataset
    3. Aggregate # Gộp kết quả   - Classification → bỏ phiếu   - Regression → lấy trung bình
Ví dụ với 10.000 dòng dữ liệu:
    10.000 dòng => Tạo 100 bộ bootstrap => Train 100 cây => Lấy trung bình kết quả
    Đó chính là cơ chế cốt lõi của Bagging, và Random Forest là ứng dụng nổi tiếng nhất của kỹ thuật này.
```
**Bagging giảm cái gì?**
```bash
Trong Machine Learning có:
    Error = Bias + Variance + Noise

Bagging chủ yếu giảm: Variance

Ví dụ:
    Decision Tree:
        - Bias thấp
        - Variance cao
    Bagging:
        - Bias gần như giữ nguyên
        - Variance giảm mạnh
=> Tổng lỗi giảm.
```
**Tại sao Bagging giảm Variance?**
```bash
- Một cây => 2.5 tỷ
- Cây khác: => 1.8 tỷ
- Cây khác: => 2.2 tỷ
Lấy trung bình: (2.5 + 1.8 + 2.2)/3 = 2.17 tỷ

Kết quả ổn định hơn.
Variance giảm.
```
**Tại sao Bagging lại hiệu quả?**
```bash
Giả sử mỗi cây là một chuyên gia. Ta hỏi:
    - Chuyên gia A → 2 tỷ
    - Chuyên gia B → 2.2 tỷ
    - Chuyên gia C → 1.8 tỷ
    - Chuyên gia D → 2.1 tỷ
Nếu lấy trung bình: ≈ 2.0 tỷ => Sai số ngẫu nhiên của từng chuyên gia sẽ triệt tiêu nhau.

Minh họa bằng dart
    - Một cây:
          X      |      |      |      O
    Có thể ném lệch khá xa tâm.

    - Nhiều cây:
     X   X   X X   X
    Lấy trung bình vị trí:
          X      |      |      |      O
=> Gần tâm hơn.
```


Bootstrap là gì?
Đây là phần đầu tiên của Bagging.
Giả sử dataset gốc:
ABCDE
Ta lấy mẫu ngẫu nhiên có hoàn lại (with replacement).
Ví dụ:
Dataset 1
ABBDE
Dataset 2
AACDE
Dataset 3
BCCEE
Chú ý:
Một dòng có thể xuất hiện nhiều lầnMột dòng có thể không xuất hiện
vì lấy mẫu có hoàn lại.

Tại sao phải làm vậy?
Mỗi dataset con sẽ hơi khác nhau.
Dataset 1↓Tree 1Dataset 2↓Tree 2Dataset 3↓Tree 3

Ví dụ trực quan
Giả sử cần dự đoán giá căn nhà mới.
Các cây dự đoán:
Tree1 → 2.0 tỷTree2 → 2.2 tỷTree3 → 1.9 tỷTree4 → 2.1 tỷTree5 → 2.0 tỷ

Aggregating
Regression:
Lấy trung bình.
(2.0 + 2.2 + 1.9 + 2.1 + 2.0)/5= 2.04 tỷ

Classification:
Lấy phiếu bầu.
Ví dụ phân loại chó/mèo:
Tree1 → ChóTree2 → ChóTree3 → MèoTree4 → ChóTree5 → Mèo
Kết quả:
Chó = 3 phiếuMèo = 2 phiếu
=> Dự đoán:
Chó
**Random Forest liên quan gì?**
```bash
Random Forest chính là:
    Bagging+Random Feature Selection

Bagging thường:
    Dataset bootstrap => Train Tree

Random Forest:
    Dataset bootstrap => Khi split node:chỉ chọn ngẫu nhiên một phần feature => Train Tree

Ví dụ: Diện tích, Số phòng, Mặt tiền, Quận, Năm xây
    Random Forest chỉ cho phép cây nhìn: Diện tích, Mặt tiền ở một lần split.
    Node khác lại được nhìn: Quận, Năm xây
    Điều này làm các cây đa dạng hơn.
```
**So sánh Bagging và Boosting**
```bash
Bagging
    - Các cây train độc lập. Tree1, Tree2, Tree3, Tree4
    - Train song song được.
Boosting
    - Các cây phụ thuộc nhau.
    - Tree1 => Tree2 sửa lỗi Tree1 => Tree3 sửa lỗi Tree2 => Tree4 sửa lỗi Tree3
    - Phải train tuần tự.
```
## Boosting
Boosting là một họ thuật toán (framework/ý tưởng), còn Gradient Boosting là một thuật toán cụ thể thuộc họ Boosting.
Quan hệ giống như:
Machine Learning│├── Linear Regression├── Decision Tree├── SVM└── Boosting     │     ├── AdaBoost     ├── Gradient Boosting     ├── XGBoost     ├── LightGBM     └── CatBoost

1. Boosting là gì?
Ý tưởng của Boosting:

Kết hợp nhiều mô hình yếu (weak learners) để tạo thành một mô hình mạnh.

Thông thường weak learner là:
Decision Tree nhỏ(max_depth = 1, 2, 3)
Boosting hoạt động tuần tự:
Model 1   ↓Model 2 sửa lỗi của Model 1   ↓Model 3 sửa lỗi của Model 2   ↓...
Cuối cùng cộng kết quả lại.

Ví dụ:
Dự đoán giá nhà.
Tree đầu tiên dự đoán:
100 triệu
Giá thật:
120 triệu
Sai:
+20 triệu
Tree thứ hai học phần sai đó:
+15 triệu
Còn sai:
+5 triệu
Tree thứ ba học tiếp:
+4 triệu
Kết quả cuối:
100 + 15 + 4= 119 triệu

2. AdaBoost (Boosting đời đầu)
Thuật toán Boosting nổi tiếng đầu tiên là:
AdaBoost
Ý tưởng:


Dữ liệu bị dự đoán sai sẽ được tăng trọng số.


Các mẫu khó sẽ được chú ý nhiều hơn ở vòng sau.


Ví dụ:
Mẫu A: dự đoán đúng→ giảm trọng sốMẫu B: dự đoán sai→ tăng trọng số
Tree tiếp theo tập trung học mẫu B.

3. Gradient Boosting là gì?
Gradient Boosting là một loại Boosting khác.
Nó không dùng trọng số mẫu như AdaBoost.
Thay vào đó:

Mỗi cây mới sẽ học phần lỗi (residual) của mô hình hiện tại.


Ví dụ:
Giá nhà thật:
120
Tree 1 dự đoán:
100
Residual:
120 - 100 = 20
Tree 2 học:
20
Dự đoán mới:
100 + 20 = 120

Tại sao gọi là Gradient?
Vì về mặt toán học, nó đang tối ưu hàm mất mát bằng cách đi theo hướng:
Negative Gradient
giống Gradient Descent.
Ý tưởng cốt lõi là:
Tree mới ≈ Gradient của Loss
Nên gọi là Gradient Boosting.

4. Công thức trực quan
Giả sử đã có mô hình:
F₀(x)
Sau khi thêm cây thứ nhất:
F₁(x) = F₀(x) + Tree₁(x)
Sau khi thêm cây thứ hai:
F₂(x) = F₁(x) + Tree₂(x)
Tiếp tục:
Fₘ(x) = Fₘ₋₁(x) + Treeₘ(x)
Mỗi cây chỉ học phần sai còn lại.

5. XGBoost, LightGBM, CatBoost là gì?
Đều là các phiên bản cải tiến của Gradient Boosting.
XGBoost
Thêm:


Regularization


Pruning


Parallelization


Nhanh và chính xác hơn Gradient Boosting gốc.

LightGBM
Tối ưu cho:
Dataset lớn
Rất nhanh.

CatBoost
Tối ưu cho:
Categorical features
Ví dụ:
Giới tínhThành phốNghề nghiệp

Tóm tắt
Khái niệmÝ nghĩaBoostingÝ tưởng tổng quát: nhiều mô hình yếu học tuần tự để sửa lỗi nhauAdaBoostMột thuật toán Boosting dùng trọng số mẫuGradient BoostingMột thuật toán Boosting dùng gradient/residual để sửa lỗiXGBoostPhiên bản nâng cấp của Gradient BoostingLightGBMGradient Boosting tối ưu tốc độCatBoostGradient Boosting tối ưu dữ liệu categorical
Nói ngắn gọn:

Boosting là "gia đình", Gradient Boosting là một "thành viên" trong gia đình đó. AdaBoost, Gradient Boosting, XGBoost, LightGBM, CatBoost đều thuộc nhóm Boosting.

**Tại sao Boosting giảm Bias?**
```bash
Giả sử cây đầu:
    - Dự đoán 2 tỷ
    - Thực tế 3 tỷ
    - Sai: +1 tỷ

Cây sau học phần sai:
    - +0.8 tỷ

Cây sau nữa:
    - +0.15 tỷ

Sai số ngày càng nhỏ.
=> Bias giảm.
```
## Gradient Boosting 
```bash
không phải là một mô hình cụ thể.
Nó là một framework / kỹ thuật xây dựng mô hình (ensemble method).

Ví dụ dễ hiểu
Giả sử bạn muốn dự đoán giá nhà.
Bạn xây cây quyết định đầu tiên:
Tree 1
Dự đoán:
Giá thậtDự đoán2 tỷ1.8 tỷ3 tỷ2.5 tỷ4 tỷ4.2 tỷ
Nó vẫn còn sai.
Sai số:
Giá thậtDự đoánError2 tỷ1.8 tỷ+0.23 tỷ2.5 tỷ+0.54 tỷ4.2 tỷ-0.2

Gradient Boosting nói:

Đừng xây cây thứ hai để dự đoán giá nhà nữa.
Hãy xây cây thứ hai để học phần sai số của cây thứ nhất.


Tree 2 học:
+0.2+0.5-0.2
Sau đó:
Prediction = Tree1 + Tree2

Vẫn còn sai?
Lại xây Tree 3 học phần sai còn lại.
Prediction= Tree1+ Tree2+ Tree3

Cứ lặp đi lặp lại:
Prediction =Tree1+ Tree2+ Tree3+ ...+ TreeN
Mỗi cây mới sửa lỗi cho các cây trước.
Đó chính là ý tưởng của Boosting.

Tại sao gọi là "Gradient" Boosting?
Ban đầu có thuật toán Boosting đơn giản là AdaBoost.
Sau này người ta nhận ra:

Việc tìm lỗi để sửa có thể được diễn tả bằng Gradient Descent.

Giống như Neural Network:
Loss↓Tính gradient↓Update tham số

Gradient Boosting cũng vậy.
Ở mỗi bước:
Loss↓Tính gradient của loss↓Huấn luyện cây mới để học gradient đó↓Cập nhật mô hình
Nên mới có tên:
Gradient Boosting

Công thức trực quan
Giả sử:
Giá thật = yDự đoán = ŷ
Mô hình ban đầu:
F0(x)
Sau cây đầu tiên:
F1(x) = F0(x) + Tree1(x)
Sau cây thứ hai:
F2(x) = F1(x) + Tree2(x)
...
Sau N cây:
FN(x)=F0(x)+Σ Tree_i(x)

Vậy XGBoost và LightGBM là gì?
Chúng đều là các triển khai của Gradient Boosting.
Gradient Boosting│├── GBM (bản gốc)│├── XGBoost│├── LightGBM│└── CatBoost
Có thể hình dung:
Gradient Boosting
là ý tưởng.
Còn:


XGBoost


LightGBM


CatBoost


là các phiên bản hiện thực hóa ý tưởng đó.
Giống như:
Neural Network
là ý tưởng.
Còn:


PyTorch


TensorFlow


là công cụ triển khai.

Random Forest có phải Gradient Boosting không?
Không.
Đây là hai họ thuật toán khác nhau.
Random Forest
Các cây hoạt động độc lập.
Tree1Tree2Tree3Tree4
Cuối cùng lấy trung bình:
Prediction=Average(Tree1, Tree2, Tree3, Tree4)

Gradient Boosting
Các cây phụ thuộc nhau.
Tree1↓ sửa lỗiTree2↓ sửa lỗiTree3↓ sửa lỗiTree4
Mỗi cây được tạo ra vì cây trước còn sai.

Cách nhớ nhanh


Decision Tree → một cây.


Random Forest → nhiều cây độc lập rồi lấy trung bình.


Gradient Boosting → nhiều cây nối tiếp nhau, cây sau sửa lỗi cây trước.


XGBoost / LightGBM / CatBoost → các phiên bản tối ưu của Gradient Boosting.


Nói ngắn gọn: Gradient Boosting là một thuật toán học tăng cường theo kiểu ensemble, không phải một mô hình cụ thể. Kết quả cuối cùng là một mô hình gồm nhiều cây quyết định được cộng lại với nhau.
```