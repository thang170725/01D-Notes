- [Preprocessing](#preprocessing)
  - [train\_test\_split()](#train_test_split)
- [StandardScaler()](#standardscaler)
- [preprocessing (Tiền xử lý)](#preprocessing-tiền-xử-lý)
  - [LabelEncoder() (chuyển đổi các giá trị thành các số nguyên)](#labelencoder-chuyển-đổi-các-giá-trị-thành-các-số-nguyên)
- [Pipeline](#pipeline)
- [CountVectorizer()](#countvectorizer)
- [.inverse\_transform() (Để giải mã)](#inverse_transform-để-giải-mã)
- [.class\_ (In ra tất cả các giá trị khác nhau của intent. Các giá trị tạo thành một mảng)](#class_-in-ra-tất-cả-các-giá-trị-khác-nhau-của-intent-các-giá-trị-tạo-thành-một-mảng)
- [model\_selection](#model_selection)
- [tree (Cây quyết định)](#tree-cây-quyết-định)
  - [DecisionTreeClassifier() (một cây quyết định)](#decisiontreeclassifier-một-cây-quyết-định)
  - [plot\_tree() (Để vẽ cây quyết định)](#plot_tree-để-vẽ-cây-quyết-định)
- [Datasets (bộ dữ liệu có sẵn trong scikit-learn)](#datasets-bộ-dữ-liệu-có-sẵn-trong-scikit-learn)
  - [load\_digits()](#load_digits)
    - [.keys()](#keys)
  - [.images\[\]](#images)
  - [.reshape()](#reshape)
  - [Target (Nhãn tương ứng với từng ảnh - số 0 đến số 9)](#target-nhãn-tương-ứng-với-từng-ảnh---số-0-đến-số-9)
  - [Data (Ảnh những được làm phẳng (flatten) thành vector 1 chiều có 64 phần tử)](#data-ảnh-những-được-làm-phẳng-flatten-thành-vector-1-chiều-có-64-phần-tử)
  - [make\_blobs (tạo dữ liệu giả lập cho các bài toán phân cụm hoặc phân loại)](#make_blobs-tạo-dữ-liệu-giả-lập-cho-các-bài-toán-phân-cụm-hoặc-phân-loại)
- [cluster](#cluster)
  - [.Kmeans()](#kmeans)
- [Bootstrapping: lấy 1000 mẫu, mỗi mẫu có 20 phần tử](#bootstrapping-lấy-1000-mẫu-mỗi-mẫu-có-20-phần-tử)
- [Tính khoảng tin cậy 80% (10% và 90% phân vị)](#tính-khoảng-tin-cậy-80-10-và-90-phân-vị)
- [Vẽ đồ thị phân phối của các trung bình mẫu](#vẽ-đồ-thị-phân-phối-của-các-trung-bình-mẫu)
- [impute](#impute)
  - [SimpleImputer  (dùng để điền giá trị bị thiếu (NaN) vào dữ liệu)](#simpleimputer--dùng-để-điền-giá-trị-bị-thiếu-nan-vào-dữ-liệu)
- [Train (train model)](#train-train-model)
  - [.fit() \& .transfrom()](#fit--transfrom)
  - [.fit\_transform() (kết hợp 2 bước fit và transform)](#fit_transform-kết-hợp-2-bước-fit-và-transform)
---
# Preprocessing
## train_test_split()
```bash
- Để chia dữ liệu thành 2 phần: 
    + tập huấn luyên (training set) dùng để dạy mô hình
    + tập kiểm tra (test set) dùng để đánh giá mô hình sau khi huấn luyện.
- Rất quan trọng trong học máy để đảm bảo mô hình không bị học thuộc lòng toàn bộ dữ liệu.
```
**Syn**
```bash
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=..., random_state=…, stratify=)

- X: Dữ liệu đầu vào (features).
- y: Nhãn tương ứng (labels).
- test_size: Tỉ lệ dữ liệu để làm tập kiểm tra (0.2 = 20%).
- random_state: Giúp kết quả chia ngẫu nhiên được cố định (dễ tái lập).
```
**Ex**
```bash
from sklearn.model_selection import train_test_split

X = [[160], [165], [170], [175], [180], [185]] # X là chiều cao, y là cân nặng
y = ['nữ', 'nữ', 'nam', 'nam', 'nam', 'nam']   # chia dữ liệu thành 70% train, 30% test

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=2)

print("dữ liệu huấn luyên ", X_train) # dữ liệu huấn luyên  [[175], [170], [185], [160]]
print("nhãn huấn luyên ", y_train)    # nhãn huấn luyên  ['nam', 'nam', 'nam', 'nữ']
print("dữ liệu kiểm tra ", X_test)    # dữ liệu kiểm tra  [[180], [165]]
print("nhãn kiểm tra ", y_test)       # nhãn kiểm tra  ['nam', 'nữ']
```
# StandardScaler()
```bash
- Dùng để chuẩn hóa dữ liệu. Trả về một đối tượng Scaler với các phương thức để chuyển đổi tập dữ liệu.
- Tập dữ liệu có nhiều đơn vị khác nhau lên cần chuẩn hóa dữ liệu tránh độ lệch quá lớn.
```
**Ex1**
```bash
- Có thể khó để so sánh thể tích 1,0 với trọng lượng 790, nhưng nếu chúng ta chia tỷ lệ cả hai thành các giá trị tương đương, chúng ta có thể dễ dàng thấy giá trị này được so sánh với giá trị kia như thế nào.
- Có nhiều phương pháp khác nhau để chia tỷ lệ dữ liệu, trong hướng dẫn này, chúng ta sẽ sử dụng một phương pháp gọi là chuẩn hóa.
- Phương pháp chuẩn hóa sử dụng công thức này: z = (x - u) / s
    + z : là giá trị mới
    + x : là giá trị ban đầu
    + u : là giá trị trung bình
    + s : là độ lệch chuẩn.
```
**Ex**
```python
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

df = pandas.read_csv("data.csv")
X = df[['Weight', 'Volume']]

scaledX = scale.fit_transform(X)

print(scaledX)
# [[-2.10389253 -1.59336644]
#  [-0.55407235 -1.07190106]
#  [-1.52166278 -1.59336644]
#  ...
#  [ 0.40932938 -0.0289703 ]
#  [ 0.47215993 -0.0289703 ]
#  [ 0.4302729   2.31762392]]
```
# preprocessing (Tiền xử lý)
## LabelEncoder() (chuyển đổi các giá trị thành các số nguyên)
**Syn**
```bash
from sklearn.preprocessing import LabelEncoder

# 1. tạo LabelEncoder
le = LabelEncoder()
# 2. mã hóa từ chuỗi sang số
encoded = le.fit_transform(arr)
```
**Ex1**
```python
from sklearn.preprocessing import LabelEncoder

arr = ['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue'] # dữ liệu gốc dạng chuỗi

le = LabelEncoder()# tạo LabelEncoder

encoded = le.fit_transform(arr) # mã hóa từ chuỗi sang số

print(arr, encoded) # ['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue'] [2 0 0 1 3 4 0]
```
**Ex2**
```python
from sklearn.preprocessing import LabelEncoder
import pandas as pd
# dữ liệu gốc dạng chuỗi
arr = pd.DataFrame(
    {
        'city': ['hanoi', 'hcm', 'da nang', 'da nang', 'hue']
    }
)

le = LabelEncoder() # tạo LabelEncoder

arr['encode city'] = le.fit_transform(arr['city']) # mã hóa từ chuỗi sang số

print(arr)

#       city  encode city
# 0    hanoi            1
# 1      hcm            2
# 2  da nang            0
# 3  da nang            0
# 4      hue            3
```
# Pipeline
```bash
Chuỗi các bước xử lý dữ liệu + model
```
**Syn**
```bash
from sklearn.pipeline import Pipeline

pipe = Pipeline(steps=[
    ("tên_bước_1", transformer),
    ("tên_bước_2", model)
])
```
**Ex: Chuẩn hóa dữ liệu +  Logistic Regression**
```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.datasets import load_iris

# Load data
X, y = load_iris(return_X_y=True)

# Train / test split
X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

# Tạo pipeline
pipe = Pipeline([
    ("scaler", StandardScaler()),
    ("model", LogisticRegression())
])

# Train
pipe.fit(X_train, y_train)

# Predict
y_pred = pipe.predict(X_test)

# Score
print("Accuracy:", pipe.score(X_test, y_test))

# Không cần gọi scaler.fit_transform() thủ công Pipeline tự xử lý thứ tự chuẩn.
```
# CountVectorizer()
```bash
Công cụ tự động hóa việc: Tách từ (tokenize), Xây dựng từ vựng (vocabulary), Đếm số lần xuất hiện của từng từ trong mỗi tài liệu
```
**Ex**
```python
vectorizer = CountVectorizer()
X = vectorizer.fit_transform(self.df["text"]).toarray()
```

.get_feature_names_out()
Xem danh sách từ vựng.
.toarray()
Xem ma trận đếm
```bash
from sklearn.linear_model import LinearRegression
```
# .inverse_transform() (Để giải mã)
# .class_ (In ra tất cả các giá trị khác nhau của intent. Các giá trị tạo thành một mảng)
**Ex**
```python
print(label_encoder.classes_)
# ['close_info' 'greeting' 'open_info' 'open_webapp' 'play_music', 'stop_music' 'turn_off_lights' 'turn_on_lights' 'weather']
```
# model_selection
# tree (Cây quyết định)
## DecisionTreeClassifier() (một cây quyết định)
```bash
Là một mô hình học máy thuộc loại phân loại (classification) 
    dùng để dự đoán đối tượng thuộc về nhóm nào (label/class), dựa trên các đặc điểm (features) của nó.

Nó hoạt động như một cây quyết định, ở mỗi nút, nó đặt câu hỏi “có hay không”, nhỏ hơn bao nhiêu” rồi phân nhánh.
```
**Syn**
```bash
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(criterion='gini', max_depth=None, random_state=None)

- criterion: Tiêu chí chia nhánh.
- max_depth: Giới hạn độ sâu của cây.
- random_state: Đảm bảo kết quả lặp lại khi chạy nhiều lần.
```
## plot_tree() (Để vẽ cây quyết định)
# Datasets (bộ dữ liệu có sẵn trong scikit-learn) 
## load_digits()
```bash
- Là một bộ dữ liệu datasets có sẵn trong thư viện scikit-learn.
- Dùng để huấn luyện mô hình phân loại chữ số viết tay (0-9). Bộ dữ liệu này rất phù hợp để học máy vì nó có kích thước nhỏ, dễ thao tác và tiền xử lý tốt.
```
**Ex**
```python
from sklearn.datasets import load_digits
digits = load_digits()

# digits là một object chứa dữ liệu ảnh số viết tay
# đây là một dữ liệu nhỏ, mỗi ảnh có kích thước 8x8 pixel (nhỏ hơn MNIST 28x28)
```
### .keys()
```bash
- Để xem dữ liệu bên trong object digits.
```
**Ex**
```python
from sklearn.datasets import load_digits
digits = load_digits()

print(digits.keys()) # dict_keys(['data', 'target', 'frame', 'feature_names', 'target_names', 'images', 'DESCR'])
```
## .images[]
```bash
- Danh sách ảnh dạng 2D (ma trận 8x8 pixels).
```
**Ex**
```python
from sklearn.datasets import load_digits
import matplotlib.pyplot as 

digits = load_digits()

plt.imshow(digits.images[0], cmap='gray')
plt.title(f'{digits.target[0]}')
plt.show()
# ảnh số 0 sẽ hiện ra
```
## .reshape()
```bash
Mạng nơ ron không xử lý được ảnh 2d, nó cần một vector 1d. ta chuyển ảnh thành vector có 64 phần tử.
```
**Ex**
```python
from sklearn.datasets import load_digits
import matplotlib.pyplot as plt

digits = load_digits()

X = digits.images.reshape((len(digits.images), -1))
y = digits.target

print(X)
print(y.shape)

# [[ 0.  0.  5. ...  0.  0.  0.]
#  [ 0.  0.  0. ... 10.  0.  0.]
#  [ 0.  0.  0. ... 16.  9.  0.]
#  ...
#  [ 0.  0.  1. ...  6.  0.  0.]
#  [ 0.  0.  2. ... 12.  0.  0.]
#  [ 0.  0. 10. ... 12.  1.  0.]]
(1797,)
```
## Target (Nhãn tương ứng với từng ảnh - số 0 đến số 9)
## Data (Ảnh những được làm phẳng (flatten) thành vector 1 chiều có 64 phần tử)
## make_blobs (tạo dữ liệu giả lập cho các bài toán phân cụm hoặc phân loại)
```bash
Dùng để . Dữ liệu tạo ra gồm các điểm dữ liệu được phân bố quanh các tâm cụm xác định, rất hữu ích cho việc thử nghiệm mô hình học máy.
```
**Syn**
```python
from sklearn.datasets import make_blobs

X, y = make_blobs(n_samples=100,       # số lượng điểm dữ liệu
                  n_features=2,        # số đặc trưng (feature)
                  centers=3,           # số cụm hoặc tọa độ cụm
                  cluster_std=1.0,     # độ lệch chuẩn (spread) của cụm
                  random_state=42)     # seed để kết quả giống nhau mỗi lần
- Output:
    + X: mảng numpy chứa tọa độ các điểm dữ liệu, shape=(n_samples, n_features)
    + y: mảng numpy chứa nhãn cụm tương ứng cho từng điểm, shape=(n_samples,)
```
**Ex**
```python
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

X,y = make_blobs(n_samples=300, centers=3, random_state=42)

plt.scatter(X[:,0], X[:,1], c=y, cmap='viridis')
plt.show()
```
# cluster
## .Kmeans()
**Ex**
```python
import numpy as np
from sklearn.cluster import KMeans

# 1. Chuẩn bị dữ liệu (Chuyển danh sách điểm thành Numpy Array)
X = np.array([[1, 1], [1, 3], [2, 2], [4, 4], [4, 5], [5, 4], [5, 5]])

# 2. Định nghĩa tọa độ 3 tâm cụm ban đầu (m1=x1, m2=x2, m3=x3)
# Chú ý: Cần bọc trong np.array để tương thích với scikit-learn
initial_centroids = np.array([[1, 1], [1, 3], [2, 2]])

# 3. Khởi tạo đối tượng KMeans
# n_init=1 nghĩa là chỉ chạy đúng 1 lần với tâm cụm ta đưa vào, không chạy lại ngẫu nhiên
model = KMeans(
    n_clusters=3, init=initial_centroids, n_init=1, max_iter=100
)

# 4. Hàm kích hoạt thuật toán tính toán (Thay cho toàn bộ vòng lặp for/while code thuần)
model.fit(X)

# 5. Lấy kết quả đầu ra
labels = model.labels_  # Mảng chứa kết quả gán cụm của từng điểm
final_centroids = model.cluster_centers_  # Tọa độ các tâm cụm sau khi hội tụ

# --- IN KẾT QUẢ ---
print("=== KẾT QUẢ K-MEANS BẰNG SCIKIT-LEARN ===")
print("Kết quả gán cụm của từng điểm (từ x1 đến x7):")
print(labels)
# Kết quả sẽ có dạng dạng: [0 1 2 2 2 2 2] nghĩa là x1 thuộc cụm 0, x2 thuộc cụm 1, còn lại thuộc cụm 2

print("\nTọa độ các tâm cụm cuối cùng sau khi hội tụ:")
for i, center in enumerate(final_centroids):
    print(f"  Tâm cụm {i+1}: {center}")

# === KẾT QUẢ K-MEANS BẰNG SCIKIT-LEARN ===
# Kết quả gán cụm của từng điểm (từ x1 đến x7):
# [0 1 0 2 2 2 2]

# Tọa độ các tâm cụm cuối cùng sau khi hội tụ:
#   Tâm cụm 1: [1.5 1.5]
#   Tâm cụm 2: [1. 3.]
#   Tâm cụm 3: [4.5 4.5]
```
sklearn.metrics.accuracy_score
sklearn.metrics.classification_report
sklearn.metrics.confusion_matrix
sklearn.model_selection.cross_val_score
sklearn.model_selection.GridSearchCV
Thuật toán làm sạch dữ liệu
from scipy.stats import skewnorm
import numpy as np
import matplotlib.pyplot as plt

#Đặt seed để có thể lặp lại dữ liệu
np.random.seed(42)#Khi mà ông sinh ra số ngẫu nhiên thì đến lúc mà ông bấm lại chương trình thì sô random bị thay đổi , vì vậy ta phải đặt 1 cái seed giống như là 1 cái cọc , cái chốt để lần sau mà sinh ra số ngẫu nhiên thì vẫn như vậy

a = 10 # âm thì lệch phải , 0 thì chuẩn , dương thì lệch trái

x = skewnorm.rvs(a,size=10000) + 0.5 #x là tên tập dữ liệu

list = [] #Danh sách  lưu các trung bình mẫu của mẫu ngẫu nhiên

for i in range(2000): #Tức là lấy 1000 mẫu ngẫu nhiên
    #Chạy random khoảng 30 lần tức là lấy 30 giá trị ngẫu nhiên từ trong tập dữ liệu x sau đó thêm vào list
    #Định lý giới hạn trung tâm thì càng lấy nhiều mẫu ngẫu nhiên thì càng tốt
    #Trong 1 mẫu thì sẽ có số lượng phần tử , thì n = 30 tức là có 30 phần tử
    t = [] #Lưu các giá trị ngẫu nhiên
    for j in range(30):
      t.append(np.random.choice(x))#Xong cái đoạn này là tạo xong 30 số ngẫu nhiên trong 1 mẫu ngẫu nhiên
    list.append(np.mean(t))

#Vẽ 2 cái ảnh
fig,ax = plt.subplots(1,2,figsize=(12,5)) #Cái hàm này sẽ trả về 2 thứ là 1 bức ảnh , 2 là hệ tọa độ ax
ax[0].hist(x,bins=30)
ax[0].set_title("Bieu do tan suat cua 10000 gia tri")
ax[0].set_xlabel("Gia tri")
ax[0].set_ylabel("Tan suat")

ax[1].hist(list,bins=30)
ax[1].set_title("Bieu do tan suat cua 1000 trung binh mau")
ax[1].set_xlabel("Trung binh tung mau")
ax[1].set_ylabel("Tan suat")

plt.show()
#Đắt seed để nó có thể lặp lại dữ liệu


Thuật toán bootstrapping
import numpy as np
import matplotlib.pyplot as plt

list_tb = []  # Lưu các giá trị trung bình mẫu mà mình lấy được từ mẫu
x = [160, 170, 165, 155, 180, 172, 168, 162, 176, 169, 171, 167, 164, 173, 178]

# Bootstrapping: lấy 1000 mẫu, mỗi mẫu có 20 phần tử
for i in range(1000):
    t = []  # Lưu giá trị các mẫu mà tìm được
    for j in range(20):
        t.append(np.random.choice(x))
    list_tb.append(np.mean(t))

mang = np.array(list_tb)  # Chuyển về mảng

# Tính khoảng tin cậy 80% (10% và 90% phân vị)
low = np.percentile(mang, 2.5)  # 10% phân vị (bên dưới)
high = np.percentile(mang, 97.5)  # 90% phân vị (bên trên)

print(f"Khoảng tin cậy 80% cho trung bình chiều cao: [{low:.2f} - {high:.2f}]")

# Vẽ đồ thị phân phối của các trung bình mẫu
plt.hist(mang, bins=30, edgecolor='black', alpha=0.7)
plt.axvline(x=low, color='red', linestyle='dashed', linewidth=2, label=f'10th Percentile: {low:.2f}')
plt.axvline(x=high, color='green', linestyle='dashed', linewidth=2, label=f'90th Percentile: {high:.2f}')
plt.axvline(x=np.mean(x), color='blue', linestyle='solid', linewidth=2, label=f'Mean of Sample: {np.mean(x):.2f}')
plt.title('Bootstrap Distribution of Sample Means')
plt.xlabel('Sample Mean')
plt.ylabel('Frequency')
plt.legend()
plt.show()

transform()
clip()
14.3 Thư viện neighbors 
14.2.5.1 KNN và Thư viện KneighborsClassifier
14.2.5.1.1 Giới thiệu
Ưu điểm
Nhược điểm
Trực quan, không cần huấn luyện phức tạp
Nếu dữ liệu ít KNN có thể cho ra kết quả rất tốt
Phát hiện ngoại lệ tốt, ít bị quá tự tin vào điểm lạ
Cần tính toán khoảng cách đến tất cả các điểm huấn luyện rất chậm nếu dữ liệu lớn. Không phù hợp với dữ liệu lớn.
Nếu phân bố không đều KNN dễ dự đoán sai.
Khi chiều quá lớn, khoảng cách euclid mất ý nghĩa (lời nguyền không gian)
Phải chuẩn hóa, …
14.2.5.1.2 Cơ bản
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt
import numpy as np
from sklearn.model_selection import train_test_split
from collections import Counter

X,y = make_blobs(n_samples=300, centers=3, random_state=42)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.1 ,random_state=42)

def khoang_cach(x1,x2):
    return np.sqrt(np.sum((x1-x2)**2))

def du_doan_1d(x, X_train, y_train, k):
    kc = [khoang_cach(x, x_train) for x_train in X_train]
    k_indices = np.argsort(kc)[:k]
    k_labels = [y_train[i] for i in k_indices]
    most_common = Counter(k_labels).most_common(1)
    return most_common[0][0]

def du_doan_nhieu_diem(X_test, X_train, y_train, k):
    return [du_doan_1d(x, X_train, y_train, k) for x in X_test]

k = 5
y_pred = du_doan_nhieu_diem(X_test, X_train, y_train, k)
accuracy = np.sum(np.array(y_pred) == y_test) / len(y_test)
print(f"Độ chính xác: {accuracy:.2f}")

plt.scatter(X_test[:, 0], X_test[:, 1], c=y_pred, cmap='viridis', marker='o', label='Dự đoán')
plt.scatter(X_train[:, 0], X_train[:, 1], c=y_train, cmap='viridis', marker='x', alpha=0.5, label='Huấn luyện')
plt.legend()
plt.title("KNN phân loại")
plt.show()

KneighborsClassifier()
fit()
predict()
# impute
## SimpleImputer  (dùng để điền giá trị bị thiếu (NaN) vào dữ liệu)
**Ex1: Điền bằng giá trị trung bình (mean)**
```python
Dữ liệu
import numpy as np
import pandas as pd

df = pd.DataFrame({
   "age": [20, 25, np.nan, 30, np.nan]
})

print(df)
#    age
# 0  20.0
# 1  25.0
# 2   NaN
# 3  30.0
# 4   NaN

from sklearn.impute import SimpleImputer

imputer = SimpleImputer(strategy="mean")

df["age"] = imputer.fit_transform(df[["age"]])

print(df)
#    age
# 0  20.0
# 1  25.0
# 2  25.0
# 3  30.0
# 4  25.0
# (20 + 25 + 30) / 3 = 25 nên NaN được thay bằng 25.
```
**Ex2. Điền bằng giá trị xuất hiện nhiều nhất (most_frequent)**
```python
df = pd.DataFrame({
   "city": ["HN", "HCM", np.nan, "HN", np.nan]
})

print(df)
#  city
# 0   HN
# 1  HCM
# 2  NaN
# 3   HN
# 4  NaN

imputer = SimpleImputer(strategy="most_frequent")

df["city"] = imputer.fit_transform(df[["city"]]).ravel()

print(df)
#  city
# 0   HN
# 1  HCM
# 2   HN
# 3   HN
# 4   HN
```
# Train (train model)
## .fit() & .transfrom()
```bash
- fit               : học dữ liệu.
- fit_transform     : 
```
**Syn** 
```bash
model.fit(X, y)
```
## .fit_transform() (kết hợp 2 bước fit và transform)
```bash
Yầu đầu vào là một iterable, có thể là list, numpy array, series, ...
```
predict()
Dùng để dự đoán kết quả (label/ class) của dữ liệu mới sau khi đã huấn luyện bằng fit().
Cú pháp: model.predict(X_new)