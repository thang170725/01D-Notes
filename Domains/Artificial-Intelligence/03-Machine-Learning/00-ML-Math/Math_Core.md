- [Phương sai](#phương-sai)
- [Độ lệch chuẩn tổng thể và độ lệch chuẩn mẫu](#độ-lệch-chuẩn-tổng-thể-và-độ-lệch-chuẩn-mẫu)
- [(2.5 + 1.8 + 2.2)/3](#25--18--223)
- [Computer Vision](#computer-vision)
  - [Kernel](#kernel)
  - [Gaussian Blur](#gaussian-blur)
  - [Median Blur](#median-blur)
  - [Sharpen (làm sắc nét)](#sharpen-làm-sắc-nét)
  - [Sobel, Laplacian](#sobel-laplacian)
- [clustering (gom cụm)](#clustering-gom-cụm)
- [Tree](#tree)
  - [Bagging (Bootstrap Aggregating)](#bagging-bootstrap-aggregating)
  - [Gradient Boosting](#gradient-boosting)
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
Bias và Variance là hai khái niệm cực kỳ quan trọng trong Machine Learning. Nếu hiểu được chúng, bạn sẽ hiểu vì sao:

Linear Regression đôi khi quá đơn giản.
Decision Tree đôi khi overfit.
Random Forest lại hiệu quả.
Bagging giảm variance.
Boosting giảm bias.
Ví dụ: bắn cung

Hãy tưởng tượng tâm bia là đáp án đúng.

      X
   X  O  X
      X

O = đáp án đúng

X = dự đoán của mô hình

1. Bias là gì?

Bias = mô hình lệch có hệ thống khỏi đáp án đúng.

Ví dụ:

X X X
X X X
X X X


          O

Tất cả mũi tên đều tập trung một chỗ.

Nhưng lệch xa tâm.

Điều này có nghĩa:

Mô hình học chưa đủ

Nó đang đơn giản hóa vấn đề quá mức.

Ví dụ dự đoán giá nhà

Giá thực tế:

Diện tích	Giá
50	2 tỷ
100	6 tỷ
150	15 tỷ

Quan hệ thực:

      *
          *
*

(Cong mạnh)

Nhưng bạn dùng Linear Regression:

---------

(chỉ là đường thẳng)

Nó không thể mô tả được dữ liệu.

=> Sai ở mọi nơi.

Đây là:

High Bias
Dấu hiệu

Train:

Sai

Test:

Cũng sai

Ta gọi là:

Underfitting
2. Variance là gì?

Variance = mô hình quá nhạy với dữ liệu train.

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

Đó là:

High Variance

Ví dụ bắn cung

X        X



     O


          X

 X

Các mũi tên bay lung tung.

Không ổn định.

Overfitting chính là High Variance

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

Tại sao Bagging giảm Variance?

Một cây:

2.5 tỷ

Cây khác:

1.8 tỷ

Cây khác:

2.2 tỷ

Lấy trung bình:

(2.5 + 1.8 + 2.2)/3
=
2.17 tỷ

Kết quả ổn định hơn.

Variance giảm.

Tại sao Boosting giảm Bias?

Giả sử cây đầu:

Dự đoán 2 tỷ
Thực tế 3 tỷ

Sai:

+1 tỷ

Cây sau học phần sai:

+0.8 tỷ

Cây sau nữa:

+0.15 tỷ

Sai số ngày càng nhỏ.

Bias giảm.

Câu thần chú dễ nhớ

Bias = mô hình quá ngu vì quá đơn giản

Không học đủ
↓
Underfitting

Variance = mô hình quá thông minh đến mức học thuộc

Học quá kỹ
↓
Overfitting

Vì thế người ta thường nói:

Machine Learning là bài toán cân bằng giữa Bias và Variance.

Tăng độ phức tạp mô hình → Bias giảm nhưng Variance tăng.
Giảm độ phức tạp mô hình → Variance giảm nhưng Bias tăng.

Mục tiêu là tìm điểm cân bằng sao cho mô hình vừa học đủ quy luật của dữ liệu, vừa không học thuộc dữ liệu train.
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
là một kỹ thuật ensemble rất quan trọng, và hiểu nó sẽ giúp bạn hiểu luôn Random Forest.

Vấn đề cần giải quyết
Giả sử bạn có dataset dự đoán giá nhà:
Diện tíchGiá502 tỷ602.5 tỷ703 tỷ803.5 tỷ......
Bạn huấn luyện một cây quyết định.
Cây quyết định có nhược điểm:
Rất nhạy với dữ liệu train
Chỉ cần thay đổi vài dòng dữ liệu:
Dataset A↓Tree ADataset B (khác một chút)↓Tree B
Có thể cho ra hai cây hoàn toàn khác nhau.
Ta gọi đây là high variance.

Ý tưởng của Bagging
Thay vì:
1 Dataset↓1 Tree↓Prediction
Ta làm:
1 Dataset↓Tạo nhiều dataset con↓Train nhiều cây↓Gộp kết quả

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

Tại sao Bagging lại hiệu quả?
Giả sử mỗi cây là một chuyên gia.
Ta hỏi:
Chuyên gia A → 2 tỷChuyên gia B → 2.2 tỷChuyên gia C → 1.8 tỷChuyên gia D → 2.1 tỷ
Nếu lấy trung bình:
≈ 2.0 tỷ
Sai số ngẫu nhiên của từng chuyên gia sẽ triệt tiêu nhau.

Minh họa bằng dart
Một cây:
      X      |      |      |      O
Có thể ném lệch khá xa tâm.

Nhiều cây:
 X   X   X X   X
Lấy trung bình vị trí:
      X      |      |      |      O
Gần tâm hơn.

Bagging giảm cái gì?
Trong Machine Learning có:
Error=Bias+Variance+Noise
Bagging chủ yếu giảm:
Variance

Ví dụ:
Decision Tree:
Bias thấpVariance cao
Bagging:
Bias gần như giữ nguyênVariance giảm mạnh
=> Tổng lỗi giảm.

Random Forest liên quan gì?
Random Forest chính là:
Bagging+Random Feature Selection

Bagging thường:
Dataset bootstrap↓Train Tree

Random Forest:
Dataset bootstrap↓Khi split node:chỉ chọn ngẫu nhiên một phần feature↓Train Tree
Ví dụ có:
Diện tíchSố phòngMặt tiềnQuậnNăm xây
Random Forest chỉ cho phép cây nhìn:
Diện tíchMặt tiền
ở một lần split.
Node khác lại được nhìn:
QuậnNăm xây
Điều này làm các cây đa dạng hơn.

So sánh Bagging và Boosting
Bagging
Các cây độc lập.
Tree1Tree2Tree3Tree4
Train song song được.

Boosting
Các cây phụ thuộc nhau.
Tree1↓Tree2 sửa lỗi Tree1↓Tree3 sửa lỗi Tree2↓Tree4 sửa lỗi Tree3
Phải train tuần tự.

Tóm tắt dễ nhớ
Bagging hoạt động theo 3 bước:
1. Bootstrap   Tạo nhiều dataset con bằng lấy mẫu có hoàn lại2. Train   Huấn luyện một model trên mỗi dataset3. Aggregate   Gộp kết quả   - Classification → bỏ phiếu   - Regression → lấy trung bình
Ví dụ với 10.000 dòng dữ liệu:
10.000 dòng↓Tạo 100 bộ bootstrap↓Train 100 cây↓Lấy trung bình kết quả
Đó chính là cơ chế cốt lõi của Bagging, và Random Forest là ứng dụng nổi tiếng nhất của kỹ thuật này.
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

Gini Index (hay Gini Impurity) là một thước đo dùng trong Decision Tree để đánh giá một nút có "lẫn lộn" các loại dữ liệu hay không.

Ý tưởng rất đơn giản:

Nếu một nút chỉ chứa 1 loại dữ liệu → nút đó rất "sạch" → Gini = 0.
Nếu một nút chứa nhiều loại dữ liệu trộn lẫn → Gini lớn hơn.
Khi xây cây, thuật toán sẽ chọn cách chia làm cho các nút con sạch nhất có thể (Gini nhỏ nhất).
Ví dụ dễ hiểu

Giả sử bạn có một nút gồm 10 quả:

10 quả táo 🍎
0 quả cam 🍊

Nếu nhắm mắt bốc ngẫu nhiên một quả thì chắc chắn là táo.

=> Nút hoàn toàn thuần nhất.

Gini = 0

Bây giờ có:

5 táo 🍎
5 cam 🍊

Xác suất:

Táo = 0.5
Cam = 0.5

Đây là trạng thái lẫn lộn nhất vì bạn khó đoán được loại quả.

Gini = 0.5 (cao nhất với bài toán 2 lớp)

Công thức

Với k lớp:

Gini=1−∑p
i
2
	​


Trong đó:

p
i
	​

 là tỷ lệ của lớp i.

Ví dụ:

5 táo, 5 cam:

p
tao
	​

=0.5,p
cam
	​

=0.5
Gini=1−(0.5
2
+0.5
2
)
=1−(0.25+0.25)
=0.5
Decision Tree dùng Gini như thế nào?

Giả sử bạn muốn dự đoán khách hàng có mua sản phẩm hay không.

Có hai cách chia:

Cách chia A

Nhóm 1:

9 mua
1 không mua

Nhóm 2:

8 không mua
2 mua

Hai nhóm khá "sạch".

=> Gini thấp.

Cách chia B

Nhóm 1:

5 mua
5 không mua

Nhóm 2:

4 mua
6 không mua

Hai nhóm vẫn rất lẫn lộn.

=> Gini cao.

Thuật toán sẽ chọn Cách chia A vì sau khi chia, các nhóm con dễ phân loại hơn.

Trực giác quan trọng nhất

Bạn có thể hiểu Gini là:

"Nếu tôi chọn ngẫu nhiên một mẫu trong nút này, khả năng tôi gán nhầm nhãn cho nó là bao nhiêu?"

Gini = 0 → không thể nhầm.
Gini càng lớn → dữ liệu càng lẫn lộn.
Decision Tree luôn tìm cách chia để giảm Gini nhiều nhất.

Ví dụ nhanh:

Thành phần trong nút	Gini
100% Táo	0
90% Táo, 10% Cam	0.18
80% Táo, 20% Cam	0.32
50% Táo, 50% Cam	0.50

Nhìn bảng này có thể thấy: càng gần 50-50 thì Gini càng cao, vì dữ liệu càng khó phân biệt.
XGBoost / LightGBM / CatBoost → các phiên bản tối ưu của Gradient Boosting.


Nói ngắn gọn: Gradient Boosting là một thuật toán học tăng cường theo kiểu ensemble, không phải một mô hình cụ thể. Kết quả cuối cùng là một mô hình gồm nhiều cây quyết định được cộng lại với nhau.
```
