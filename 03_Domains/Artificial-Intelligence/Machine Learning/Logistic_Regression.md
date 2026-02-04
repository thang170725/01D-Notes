Logistic Regression
Bài tập
Demo logistic với numpy
import numpy as np
import matplotlib.pyplot as plt
# dữ liệu gốc
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

# phương trình đường cong được xây dựng bởi công thức logistic regression
def get_prediction(m, b, x):
return 1/(1 + np.exp(-m*x+b))

# hàm tính toán mất mát
def get_cost(y, y_hat):
    k = y.shape[0]
return (-1/k)*np.sum(y*np.log(y_hat)+(1-y)*np.log(1-y_hat))

# hàm cập nhật sao cho độ mất mát giảm dần
def get_gradient(m, b, x, y, y_hat):
    k = y.shape[0]
    dm = (1/k)*np.sum((y_hat - y)*x)
    db = (1/k)*np.sum(y_hat-y)
return dm, db

# hàm tính toán độ chính xác khi áp dụng lên bộ dữ liệu này
def get_accuracy(y, y_hat):
return ((y_hat >= 0.5).astype(int) == y).sum()/ y.shape[0]

# test mô hình
# 1 - bịa ra giá trị m, b
m = 1.0
b = 10.0
# số lần lặp lại để cập nhật lại độ mất mát
interations = 150
# learning rate - tốc độ cập nhật độ mất mát
lr = 0.03

x = dataSet[:, 0]
y = dataSet[:, 1]
# lưu cost vào một mảng
costs = []
for it in range(interations):
    y_hat = get_prediction(m, b, x)
    cost = get_cost(y, y_hat)
    # mức độ chính xác
    accuracy = get_accuracy(y, y_hat)
    print(f"iteration {it} - cost {cost}, accuracy: {accuracy}")
    dm, dn = get_gradient(m, b, x, y, y_hat)
    # cập nhật
    m -= lr*dm
    b -= lr*dn
    costs.append(cost)

iteration 0 - cost 1.2806026124548595, accuracy: 0.6363636363636364
iteration 1 - cost 1.0864043766201612, accuracy: 0.6363636363636364
iteration 2 - cost 0.9378122484032957, accuracy: 0.7272727272727273
…
…
iteration 143 - cost 0.013258107606832945, accuracy: 1.0
iteration 144 - cost 0.013141438742927412, accuracy: 1.0
iteration 145 - cost 0.013026711929090811, accuracy: 1.0
iteration 146 - cost 0.012913880600277159, accuracy: 1.0
iteration 147 - cost 0.012802899632104342, accuracy: 1.0
iteration 148 - cost 0.012693725286686972, accuracy: 1.0
iteration 149 - cost 0.012586315160851966, accuracy: 1.0
Demo Logistic với torch