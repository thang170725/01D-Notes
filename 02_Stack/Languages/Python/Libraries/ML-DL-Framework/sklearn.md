Sklearn
feature_extraction
text
CountVectorizer()
Công cụ tự động hóa việc: Tách từ (tokenize), Xây dựng từ vựng (vocabulary), Đếm số lần xuất hiện của từng từ trong mỗi tài liệu
Cú pháp:
self.vectorizer = CountVectorizer()
X = self.vectorizer.fit_transform(self.df["text"]).toarray()
.fit_transform()
Yầu đầu vào là một iterable, có thể là list, numpy array, series, ...

.get_feature_names_out()
Xem danh sách từ vựng.
.toarray()
Xem ma trận đếm
linear_model
from sklearn.linear_model import LinearRegression

LinearRegression() & .fit() & .predict()
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_test)
LogisticRegression
from sklearn.linear_model import LogisticRegression
import numpy as np

dataSet = np.array(
    [[-10, 0],
     [-5, 0],
     [-7, 0],
     [0, 0],
     [-2, 0],
     [5, 1],
     [7, 1],
     [6, 1],
     [10, 1],
     [15, 1],
     [9, 1]
     ]
)
X = dataSet[:, 0].reshape(-1, 1)
y = dataSet[:, 1]

logr = LogisticRegression()
logr.fit(X, y)
print(logr.predict(np.array([1]).reshape(-1,1)))
preprocessing
LabelEncoder()
.fit_transform()
Dùng để chuyển đổi các giá trị nhãn dạng chuỗi thành các số nguyên.
Cú pháp:
from sklearn.preprocessing import LabelEncoder
# dữ liệu gốc dạng chuỗi
arr = ['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue']
# tạo LabelEncoder
le = LabelEncoder()
# mã hóa từ chuỗi sang số
encoded = le.fit_transform(arr)
print(arr, encoded)
['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue'] [2 0 0 1 3 4 0]
from sklearn.preprocessing import LabelEncoder
import pandas as pd
# dữ liệu gốc dạng chuỗi
arr = pd.DataFrame(
    {
        'city': ['hanoi', 'hcm', 'da nang', 'da nang', 'hue']
    }
)
# tạo LabelEncoder
le = LabelEncoder()
# mã hóa từ chuỗi sang số
arr['encode city'] = le.fit_transform(arr['city'])

print(arr)
      city  encode city
0    hanoi            1
1      hcm            2
2  da nang            0
3  da nang            0
4      hue            3
.inverse_transform()
Để giải mã.
Cú pháp:
from sklearn.preprocessing import LabelEncoder
# dữ liệu gốc dạng chuỗi
arr = ['reb', 'blue', 'blue', 'orange', 'red', 'yellow', 'blue']
# tạo LabelEncoder
le = LabelEncoder()
# mã hóa từ chuỗi sang số
encoded = le.fit_transform(arr)
# giải mã
decoded = le.inverse_transform(encoded)
print(decoded)
['reb' 'blue' 'blue' 'orange' 'red' 'yellow' 'blue']
.class_
In ra tất cả các giá trị khác nhau của intent. Các giá trị tạo thành một mảng.
Cú pháp:
print(label_encoder.classes_)
['close_info' 'greeting' 'open_info' 'open_webapp' 'play_music', 'stop_music' 'turn_off_lights' 'turn_on_lights' 'weather']
In bảng ánh xạ nhãn
print(dict(zip(label_encoder.classes_, label_encoder.transform(label_encoder.classes_))))
model_selection
train_test_split()
    • Để chia dữ liệu thành 2 phần: tập huấn luyên (training set) dùng để dạy mô hình, tập kiểm tra (test set) dùng để đánh giá mô hình sau khi huấn luyện.
    • Cần from sklearn.model_selection import train_test_split.
    • Rất quan trọng trong học máy để đảm bảo mô hình không bị học thuộc lòng toàn bộ dữ liệu.
Cú pháp: 
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=..., random_state=…, stratify=)
    • X: Dữ liệu đầu vào (features).
    • y: Nhãn tương ứng (labels).
    • test_size: Tỉ lệ dữ liệu để làm tập kiểm tra (0.2 = 20%).
    • random_state: Giúp kết quả chia ngẫu nhiên được cố định (dễ tái lập).
from sklearn.model_selection import train_test_split
# X là chiều cao, y là cân nặng
X = [[160], [165], [170], [175], [180], [185]]
y = ['nữ', 'nữ', 'nam', 'nam', 'nam', 'nam']
# chia dữ liệu thành 70% train, 30% test
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=2)
print("dữ liệu huấn luyên ", X_train)
print("nhãn huấn luyên ", y_train)
print("dữ liệu kiểm tra ", X_test)
print("nhãn kiểm tra ", y_test)
dữ liệu huấn luyên  [[175], [170], [185], [160]]
nhãn huấn luyên  ['nam', 'nam', 'nam', 'nữ']
dữ liệu kiểm tra  [[180], [165]]
nhãn kiểm tra  ['nam', 'nữ']
14.4 Thư viện tree
14.4.1 Giới thiệu
    • Cây quyết định là biểu đồ luồng và có thể giúp bạn đưa ra quyết định dựa trên kinh nghiệm trước đó.
Thuật toán
import numpy as np

def entropy(y):
    counts = np.bincount(y)
    probs = counts / len(y)
    ent = 0
    for p in probs:
        if p > 0:
            ent -= p * np.log2(p)
    return ent

def best_split(X, y):
    m, n = X.shape
    base_entropy = entropy(y)
    best_gain = 0
    best_feature = None
    best_threshold = None

    for feature in range(n):
        values = np.unique(X[:, feature])
        for threshold in values:
            left_mask = X[:, feature] <= threshold
            right_mask = X[:, feature] > threshold

            if sum(left_mask) == 0 or sum(right_mask) == 0:
                continue

            left_entropy = entropy(y[left_mask])
            right_entropy = entropy(y[right_mask])
            weighted_entropy = (sum(left_mask) * left_entropy + sum(right_mask) * right_entropy) / m

            info_gain = base_entropy - weighted_entropy

            print(f"Feature {feature}, Threshold {threshold}, Info Gain {info_gain:.4f}")

            if info_gain > best_gain:
                best_gain = info_gain
                best_feature = feature
                best_threshold = threshold

    return best_feature, best_threshold

def build_tree(X, y, depth=0, max_depth=2):
    if len(set(y)) == 1:
        return {'leaf': True, 'class': y[0]}
    if depth >= max_depth:
        counts = np.bincount(y)
        return {'leaf': True, 'class': np.argmax(counts)}

    feature, threshold = best_split(X, y)
    if feature is None:
        counts = np.bincount(y)
        return {'leaf': True, 'class': np.argmax(counts)}

    left_mask = X[:, feature] <= threshold
    right_mask = X[:, feature] > threshold

    left_subtree = build_tree(X[left_mask], y[left_mask], depth + 1, max_depth)
    right_subtree = build_tree(X[right_mask], y[right_mask], depth + 1, max_depth)

    return {
        'leaf': False,
        'feature': feature,
        'threshold': threshold,
        'left': left_subtree,
        'right': right_subtree
    }

def predict_one(x, tree):
    if tree['leaf']:
        return tree['class']
    if x[tree['feature']] <= tree['threshold']:
        return predict_one(x, tree['left'])
    else:
        return predict_one(x, tree['right'])

def predict(X, tree):
    return np.array([predict_one(x, tree) for x in X])

# Data
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([0, 0, 1, 1, 1])

# Build tree
tree = build_tree(X, y, max_depth=2)

# Predict
print(predict(np.array([[1.5], [3.5], [4.5]]), tree))
Feature 0, Threshold 1, Info Gain 0.3219
Feature 0, Threshold 2, Info Gain 0.9710
Feature 0, Threshold 3, Info Gain 0.4200
Feature 0, Threshold 4, Info Gain 0.1710
[0 1 1]

DecisionTreeClassifier()
    • Là một mô hình học máy thuộc loại phân loại (classification) dùng để dự đoán đối tượng thuộc về nhóm nào (label/class), dựa trên các đặc điểm (features) của nó.
    • Nó hoạt động như một cây quyết định, ở mỗi nút, nó đặt câu hỏi “có hay không”, nhỏ hơn bao nhiêu” rồi phân nhánh.
    • Thường đi kèm với predict().
Cú pháp:
from sklearn.tree import DecisionTreeClassifier
model = DecisionTreeClassifier(criterion='gini', max_depth=None, random_state=None)
    • criterion: Tiêu chí chia nhánh.
    • max_depth: Giới hạn độ sâu của cây.
    • random_state: Đảm bảo kết quả lặp lại khi chạy nhiều lần.
fit() 
    • Dùng để huấn luyên mô hình học máy, tức là cho mô hình học từ dữ liệu đầu vào và nhãn đầu ra.
    • Sau khi gọi fit(), mô hình học được quy luật từ dữ liệu để sẵn sàng dự đoán cho dữ liệu mới.
Cú pháp: model.fit(X, y)
predict()
Dùng để dự đoán kết quả (label/ class) của dữ liệu mới sau khi đã huấn luyện bằng fit().
Cú pháp: model.predict(X_new)
plot_tree()
Để vẽ cây quyết định.
from sklearn.tree import DecisionTreeClassifier, plot_tree
import matplotlib.pyplot as plt
# (0: xanh, nhỏ) (1: đỏ, to)
X = [[0,1],[1,1],[0,0],[1,0]] # đặc trưng
y = [0,1,0,1] # nhãn 0 = không phải táo, 1 = táo

model = DecisionTreeClassifier()
model.fit(X,y)
print(model.predict([[1,0]]))
plot_tree(model, filled=True)
plt.show()

14.5.1 Naive bayes
14.5.1.1 Cơ bản
Naive Bayes Là một mô hình phân loại dựa trên định lý Bayes và giả định độc lập có điều kiện giữa các đặc trưng.

Thuật toán
import numpy as np

# X: mỗi hàng là 1 email, mỗi cột là đặc trưng: "free", "win", "click"
X_train = np.array([
    [1, 1, 1],  # spam
    [1, 1, 0],  # spam
    [1, 0, 1],  # spam
    [0, 1, 1],  # spam
    [1, 0, 0],  # spam
    [0, 0, 1],  # spam
    [0, 1, 0],  # not spam
    [0, 0, 0],  # not spam
    [0, 0, 1],  # not spam
    [0, 1, 1],  # not spam
])

# Nhãn: 1 = spam, 0 = not spam
y_train = np.array([1, 1, 1, 1, 1, 1, 0, 0, 0, 0])

def train_naive_bayes(X, y):
    n_samples, n_features = X.shape
    classes = np.unique(y)
    n_classes = len(classes)

    priors = np.zeros(n_classes)
    likelihoods = np.zeros((n_classes, n_features))
    for cls in classes:
        X_cls = X[y == cls]
        priors[cls] = X_cls.shape[0] / n_samples
        likelihoods[cls] = (X_cls.sum(axis=0) + 1) / (X_cls.shape[0] + 2)  # Laplace smoothing

    return priors, likelihoods

def predict_naive_bayes(X_test, priors, likelihoods):
    log_probs = []
    for cls in range(len(priors)):
        log_prior = np.log(priors[cls])
        log_likelihood = X_test * np.log(likelihoods[cls]) + (1 - X_test) * np.log(1 - likelihoods[cls])
        log_probs.append(log_prior + log_likelihood.sum(axis=1))
    return np.argmax(np.stack(log_probs, axis=1), axis=1)

# Huấn luyện
priors, likelihoods = train_naive_bayes(X_train, y_train)

# Dự đoán trên tập huấn luyện
y_pred = predict_naive_bayes(X_train, priors, likelihoods)

# Độ chính xác
accuracy = np.mean(y_pred == y_train)
print("Accuracy:", accuracy)

# Ví dụ: Email mới có "free" và "click", không có "win"
X_new = np.array([[1, 0, 1]])
y_new_pred = predict_naive_bayes(X_new, priors, likelihoods)
print("Dự đoán: Spam" if y_new_pred[0] == 1 else "Dự đoán: Không Spam")

13.4.2 Thư viện StandardScaler
Dùng để chuẩn hóa dữ liệu. Tập dữ liệu có nhiều đơn vị khác nhau lên cần chuẩn hóa dữ liệu tránh độ lệch quá lớn.
Scale
    • Được sử dụng khi dữ liệu có các giá trị khác nhau, thậm chí là các đơn vị đo lường khác nhau, việc so sánh chúng có thể rất khó khăn. Kilogram so sánh với meter như thế nào? Hay độ cao so sánh với thời giian như thế nào?
    • Câu trả lời cho vấn để này là chia tỷ lệ dữ liệu thành các giá trị mới để dễ so sánh hơn.
Ví dụ
Hãy xem bảng bên dưới, đây là cùng một tập dữ liệu mà chúng ta đã sử dụng trong chương hồi quy bội, nhưng lần này cột thể tích chứa các giá trị tính bằng lít thay vì cm3 (1,0 thay vì 1000).
Có thể khó để so sánh thể tích 1,0 với trọng lượng 790, nhưng nếu chúng ta chia tỷ lệ cả hai thành các giá trị tương đương, chúng ta có thể dễ dàng thấy giá trị này được so sánh với giá trị kia như thế nào.
Có nhiều phương pháp khác nhau để chia tỷ lệ dữ liệu, trong hướng dẫn này, chúng ta sẽ sử dụng một phương pháp gọi là chuẩn hóa.
Phương pháp chuẩn hóa sử dụng công thức này:
z = (x - u) / s
Trong đó z là giá trị mới, x là giá trị ban đầu, u là giá trị trung bình và s là độ lệch chuẩn.
Nếu bạn lấy cột trọng số từ tập dữ liệu ở trên, giá trị đầu tiên là 790 và giá trị được chia tỷ lệ sẽ là:
(790 - 1292,23) / 238,74 = -2,1
Nếu bạn lấy cột thể tích từ tập dữ liệu ở trên, giá trị đầu tiên là 1,0 và giá trị được chia tỷ lệ sẽ là:
(1,0 - 1,61) / 0,38 = -1,59
Bây giờ bạn có thể so sánh -2,1 với -1,59 thay vì so sánh 790 với 1,0.
Bạn không phải thực hiện thủ công, mô-đun Python sklearn có một phương thức gọi là StandardScaler() trả về một đối tượng Scaler với các phương thức để chuyển đổi tập dữ liệu.
Dự đoán Lượng khí thải CO2 của một chiếc ô tô dựa trên kích thước động cơ, trọng lượng bằng Scale
Output: [107.2087328]
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]
y = df['CO2']

scaledX = scale.fit_transform(X)

regr = linear_model.LinearRegression()
regr.fit(scaledX, y)

scaled = scale.transform([[2300, 1.3]])

predictedCO2 = regr.predict([scaled[0]])
print(predictedCO2)

StandardScaler()
Trả về một đối tượng Scaler với các phương thức để chuyển đổi tập dữ liệu.
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

fit_transform()
Là phương thức kết hợp 2 bước fit()  - tính toán giá trị trung bình và độ lệch chuẩn và transform() – chuẩn hóa dữ liệu.
import pandas
from sklearn import linear_model
from sklearn.preprocessing import StandardScaler
scale = StandardScaler()

df = pandas.read_csv("data.csv")

X = df[['Weight', 'Volume']]

scaledX = scale.fit_transform(X)

print(scaledX)
[[-2.10389253 -1.59336644]
 [-0.55407235 -1.07190106]
 [-1.52166278 -1.59336644]
 [-1.78973979 -1.85409913]
 [-0.63784641 -0.28970299]
 [-1.52166278 -1.59336644]
 [-0.76769621 -0.55043568]
 [ 0.3046118  -0.28970299]
 [-0.7551301  -0.28970299]
 [-0.59595938 -0.0289703 ]
 [-1.30803892 -1.33263375]
 [-1.26615189 -0.81116837]
 [-0.7551301  -1.59336644]
 [-0.16871166 -0.0289703 ]
 [ 0.14125238 -0.0289703 ]
 [ 0.15800719 -0.0289703 ]
 [ 0.3046118  -0.0289703 ]
 [-0.05142797  1.53542584]
 [-0.72580918 -0.0289703 ]
 [ 0.14962979  1.01396046]
 [ 1.2219378  -0.0289703 ]
 [ 0.5685001   1.01396046]
 [ 0.3046118   1.27469315]
 [ 0.51404696 -0.0289703 ]
 [ 0.51404696  1.01396046]
 [ 0.72348212 -0.28970299]
 [ 0.8281997   1.01396046]
 [ 1.81254495  1.01396046]
 [ 0.96642691 -0.0289703 ]
 [ 1.72877089  1.01396046]
 [ 1.30990057  1.27469315]
 [ 1.90050772  1.01396046]
 [-0.23991961 -0.0289703 ]
 [ 0.40932938 -0.0289703 ]
 [ 0.47215993 -0.0289703 ]
 [ 0.4302729   2.31762392]]
fit_transform sẽ thực hiện các bước là tính trung bình, tính phương sai, tính độ lệch chuẩn, xem ở phần numpy để hiểu rõ hơn cách tính.
transform()
Để chuẩn hóa dữ liệu.
Metrics
    • Khi bạn gọi .predict() của các mô hình ML, nó chỉ dự đoán ra kết quả y_pred thôi. Nhưng để đánh giá mô hình có tốt hay không, bạn cần so sánh y_pred (dự đoán) với y_test (giá trị thật) và tính ra sai số như MSE, MAE, r2 score.
    • Nếu chỉ .predict() mà không tính toán gì, thì chỉ thấy ra một mớ số dự đoán, không biết mô hình giỏi hay dở, không đủ chứng minh cho người khác là mô hình mình tốt hay xấu.
accuracy_score()
    • Để đánh giá độ chính xác cho mô hình cho mô hình phân nhãn rời rạc, thường đành cho logistic. Ví dụ: Nếu có 10 câu đầu vào và mô hình đoán đúng 7 câu → accuracy = 0.7
Cú pháp: 
accuracy_score(y_test, y_pred))


13.5.2 Thư viện mean_squared_error
Là một hàm đánh giá sai số phổ biến trong học máy, đặc biệt dùng trong các bài toán hồi quy (regression).
13.5.2.2 Cơ bản
mean_squared_error()
Để đo lường độ chính xác của mô hình hồi quy. MSE càng nhỏ -> mô hình càng dự đoán sát với dữ liệu thực tế. Được dùng làm hàm mất mát (cost function) trong huấn luyện mô hình
Công thức: MSE=2
    • ytrue: Giá trị thực tế
    • ypred: giá trị dự đoán
    • n: số mẫu dữ liệu
Cú pháp:
from sklearn.metrics import mean_squared_error
mse = mean_squared_error(y_true, y_pred)
from sklearn.metrics import mean_squared_error, r2_score
y_pred = model.predict(X_test_scaled)
mse = mean_squared_error(y_test, y_pred)

13.5.3 Thư viện r2_score
13.5.3.2 Cơ bản
r2_score()
    • Là một chỉ số đánh giá độ phù hợp của mô hình hồi quy, còn được gọi là hệ số xác định (coefficient of determination).
    • r-squared đo mức độ mà mô hình giải thích được phương sai của dữ liệu thực tế.
    • Nó phản ánh mức độ liên hệ tuyến tính giữa giá trị dự đoán và giá trị thực.
Công thức:  = 1 -  
    • SSres = : Tổng bình phương sai số còn lại (residual)
    • SStot = : Tổng bình phương sai của tổng thể
Nếu:
    • =1: Mô hình dự đoán chính xác hoàn toàn.
    • =0: Mô hình dự đoán kém, không hơn trung bình.
    • <0: Mô hình tệ hơn cả việc đoán trung bình.
Cú pháp:
from sklearn.metrics import r2_score
r2 = r2_score(y_true, y_pred)
from sklearn.metrics import r2_score
y_pred = model.predict(X_test_scaled)
r2 = r2_score(y_test, y_pred)
print("R2 Score:", r2)

from sklearn.metrics import r2_score

y_true = [3, -0.5, 2, 7]
y_pred = [2.5, 0.0, 2, 8]

r2 = r2_score(y_true, y_pred)
print("R2 Score:", r2)
R2 Score: 0.9486081370449679
14.5.4 Thư viện classification_report
Được dùng để đánh giá hiệu suất của mô hình phân loại. Nó hiển thị các chỉ số quan trọng cho từng lớp như:
    • Precision: Độ chính xác (đo xem trong các dự đoán đúng cho lớp đó thì bao nhiêu là đúng thật).
    • Recall: Độ bao phủ (đo xem trong tất cả các mẫu thực sự thuộc lớp đó thì bao nhiêu được dự đoán đúng).
    • F1-score: Trung bình hài hòa giữa precision và recall.
    • Support: Số lượng mẫu thật sự thuộc mỗi lớp.
from sklearn.metrics import classification_report

y_true = [0, 1, 2, 2, 1]
y_pred = [0, 0, 2, 2, 1]

print(classification_report(y_true, y_pred))


  precision    recall  f1-score   support

           0       0.50      1.00      0.67         1
           1       1.00      0.50      0.67         2
           2       1.00      1.00      1.00         2

    accuracy                           0.80         5
   macro avg       0.83      0.83      0.78         5
weighted avg       0.90      0.80      0.80         5


14.7 Thư viện datasets 
14.7.1 Giới thiệu
14.7.2 Thư viện load_digits
14.7.2.1 Giới thiệu
Là một bộ dữ liệu datasets có sẵn trong thư viện scikit-learn, dùng để huấn luyện mô hình phân loại chữ số viết tay (0-9). Bộ dữ liệu này rất phù hợp để học máy vì nó có kích thước nhỏ, dễ thao tác và tiền xử lý tốt.
14.7.2.2 Hàm, phương thức, lớp
load_digits()
from sklearn.datasets import load_digits
digits = load_digits()

# digits là một object chứa dữ liệu ảnh số viết tay
# đây là một dữ liệu nhỏ, mỗi ảnh có kích thước 8x8 pixel (nhỏ hơn MNIST 28x28)
keys()
Để xem dữ liệu bên trong object digits.
from sklearn.datasets import load_digits
digits = load_digits()
print(digits.keys())
dict_keys(['data', 'target', 'frame', 'feature_names', 'target_names', 'images', 'DESCR'])
images[]
Danh sách ảnh dạng 2D (ma trận 8x8 pixels).
from sklearn.datasets import load_digits
import matplotlib.pyplot as plt
digits = load_digits()
plt.imshow(digits.images[0], cmap='gray')
plt.title(f'{digits.target[0]}')
plt.show()
# ảnh số 0 sẽ hiện ra
reshape()
Mạng nơ ron không xử lý được ảnh 2d, nó cần một vector 1d. ta chuyển ảnh 8x8 thanhg vector có 64 phần tử.
from sklearn.datasets import load_digits
import matplotlib.pyplot as plt
digits = load_digits()
X = digits.images.reshape((len(digits.images), -1))
y = digits.target
print(X)
print(y.shape)

[[ 0.  0.  5. ...  0.  0.  0.]
 [ 0.  0.  0. ... 10.  0.  0.]
 [ 0.  0.  0. ... 16.  9.  0.]
 ...
 [ 0.  0.  1. ...  6.  0.  0.]
 [ 0.  0.  2. ... 12.  0.  0.]
 [ 0.  0. 10. ... 12.  1.  0.]]
(1797,)

Target
Nhãn tương ứng với từng ảnh (số 0 đến số 9).
Data
Ảnh những được làm phẳng (flatten) thành vector 1 chiều có 64 phần tử.
14.7.3 Thư viện make_blobs
14.7.3.1 Giới thiệu
Dùng để tạo dữ liệu giả lập cho các bài toán phân cụm hoặc phân loại. Dữ liệu tạo ra gồm các điểm dữ liệu được phân bố quanh các tâm cụm xác định, rất hữu ích cho việc thử nghiệm mô hình học máy.
14.7.3.2 Cơ bản
make_blobs()
Cú pháp:
from sklearn.datasets import make_blobs

X, y = make_blobs(n_samples=100,       # số lượng điểm dữ liệu
                  n_features=2,        # số đặc trưng (feature)
                  centers=3,           # số cụm hoặc tọa độ cụm
                  cluster_std=1.0,     # độ lệch chuẩn (spread) của cụm
                  random_state=42)     # seed để kết quả giống nhau mỗi lần
    • X: mảng numpy chứa tọa độ các điểm dữ liệu, shape=(n_samples, n_features)
    • y: mảng numpy chứa nhãn cụm tương ứng cho từng điểm, shape=(n_samples,)
from sklearn.datasets import make_blobs
import matplotlib.pyplot as plt

X,y = make_blobs(n_samples=300, centers=3, random_state=42)

plt.scatter(X[:,0], X[:,1], c=y, cmap='viridis')
plt.show()


14.7 Confusion Matrix
    • Đây là bảng được sử dụng trong các bài toán phân loại để đánh giá lỗi trong mô hình xảy ra ở đâu.
    • Các hàng biểu diễn các lớp thực tế mà kết quả phải có được. Trong khi các cột biểu diễn các dự đoán mà chúng ta đã đưa ra. Sử dụng bảng này, bạn có thể xem dự đoán nào là sai.
    • Ma trận confusion matrix có thể được tạo bằng các dự đoán đưa ra từ hồi quy logistic.
Nó dùng để:
    • Đánh giá hiệu suất của mô hình phân loại bằng cách so sánh giữa dự đoán của mô hình và nhãn thực tế.
Giải thích ngắn gọn:

Dự đoán: Pos
Dự đoán: Neg
Thực tế: Pos
True Positive (TP)
False Negative (FN)
Thực tế: Neg
False Positive (FP)
True Negative (TN)
    • TP: Dự đoán đúng trường hợp dương.
    • TN: Dự đoán đúng trường hợp âm.
    • FP: Dự đoán sai là dương (nhầm lẫn).
    • FN: Dự đoán sai là âm (bỏ sót).
    • Accuracy: Độ chính xác tổng thể.
    • Precision: Độ chính xác khi dự đoán là dương.
    • Recall: Khả năng tìm đúng tất cả trường hợp dương.
    • F1-score: Trung bình hài hòa giữa precision và recall.
14.8 Hierarchical Clustering
    • Là học máy không giám sát.
    • Một loại phân cụm, phân cấp theo phương pháp tiếp cận từ dưới lên. Chúng ta bắt đầu bằng cách xử lý từng điểm dữ liệu như một cụm riêng. Sau đó, chúng ta kết hợp các cụm có khoảng cách ngắn nhất giữa chúng lại với nhau để tạo thành các cụm lớn hơn. Bước này được lặp lại cho đến khi tạo thành một cụm lớn chứa tất cả các điểm dữ liệu.
    • Phân cụm phân cấp yêu cầu chúng ta phải quyết định cả phương pháp khoảng cách và phương pháp liên kết. Chúng ta sẽ sử dụng khoảng cách Euclid và phương pháp liên kết Ward, phương pháp này cố gắng giảm thiểu phương sai giữa các cụm.
14.9 Grid Search
    • Một phương pháp là thử các giá trị khác nhau rồi chọn giá trị cho điểm cao nhất. Kỹ thuật này được gọi là tìm kiếm lưới. Nếu chúng ta phải chọn các giá trị cho hai hoặc nhiều tham số, chúng ta sẽ đánh giá tất cả các kết hợp của các tập giá trị, do đó tạo thành một lưới các giá trị.
    • Trước khi đi vào ví dụ, tốt nhất là bạn nên biết tham số chúng ta đang thay đổi có tác dụng gì. Các giá trị C cao hơn cho biết mô hình, dữ liệu đào tạo giống với thông tin trong thế giới thực, đặt trọng số lớn hơn vào dữ liệu đào tạo. Trong khi các giá trị C thấp hơn thì ngược lại.
    • Sử dụng tham số mặc định
    • Trước tiên, hãy xem chúng ta có thể tạo ra loại kết quả nào mà không cần tìm kiếm lưới chỉ bằng cách sử dụng các tham số cơ sở.
    • Để bắt đầu, trước tiên chúng ta phải tải tập dữ liệu mà chúng ta sẽ làm việc.
14.10 K-means
14.11 Bootstrap Aggregation
14.12 Cross Validation
14.13 AUC – ROC Curve
14.14 K-nearest neighbors
14.15 Mô hình Support Vector Machine (SVM)

sklearn.preprocessing.MinMaxScaler
fit()
sklearn.neighbors.KneighborsClassifier
sklearn.cluster.Kmeans
fit()
predict()
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