keras
    • Tensorflow.keras là API cấp cao của tensorflow, được dùng rất phổ biến trong thực tế để xây dựng, huấn luyện, đánh giá và triển khai mô hình học sâu (deep learning). Đây là công cụ chính thức của google, dễ dùng, mạnh mẽ và phù hợp với cả người mới học lẫn chuyên gia.
9.6.3.2 tensorflow.keras.models

model.compile()
Biên dịch mô hình.
Cú pháp: model.compile(optimizer, loss, metrics)
    • Optimizer: Đây là thuật toán giúp mô hình cập nhật trọng số để học tốt hơn sau mỗi lần huấn luyên.
    • Loss: Là thước đo sai số giữa dự đoán của mô hình và kết quả thật.
    • Metrics: Dùng để đo lường độ chính xác của mô hình sau mỗi epoch. Accuracy = (số dự đoán đúng)/(tổng số mẫu)
9.6.3.3 tensorflow.keras.layers
Conv2D()
Dùng để tạo các kernel lấy đặc trưng cho ảnh
Cú pháp: tf.keras.layers.Conv2D(filters= , kernel_size= , activation= , input_shape= , padding=, strides)
    • Filters: Là số lượng bộ lọc để quét ảnh, mối filter sẽ học một đặc trưng khác nhau (đường ngang, đường dọc, đường cong, …). Bạn có thể chọn bất kỳ số nào, (8,16,64,128,…) => số filters càng nhiều, model càng mạnh (học nhiều đặc trưng hơn) nhưng cững tốn RAM, GPU nhiều hợn, dễ quá tải nếu chọn lớn quá.
    • kernel_size: (3,3)
MaxPooling2D()
Giảm chiều ảnh.
Cú pháp: tf.keras.layers.MaxPooling2D(pool_size)
    • pool_zize = (2,2), (4,4), …
Flatten()
Chuyển ma trận thành vector.
Cú pháp: tf.keras.layers.Flatten()
Dense()
Fully-connected layer.
Cú pháp: tf.keras.layers.Dense(<number>, activation=)
    • Number: xác định số nút nơ ron, bạn hoàn toàn có thể đổi thành 64,256,512, … miễn là hợp lý và không quá nặng so với dung lượng máy.
Embedding()
Dùng trong NLP
Cú pháp: tf.keras.layers.Embedding(input_dim, output_dim)
LSTM()
Dùng trong NLP tuần tự.
Cú pháp: tf.keras.layers.LSTM(units)
GRU()
Dùng trong NLP tuần tự.
Cú pháp: tf.keras.layers.GRU(units)
Input()
Khai báo input tùy chỉnh.
Cú pháp: tf.keras.layers.Input()
model
API tùy chỉnh model nâng cao
model.fit()
Huấn luyện
Cú pháp: model.fit(x, y, epochs, bath_size)
model.evaluate()
Đánh giá
Cú pháp: model.evaluate(x_test, y_test)
model.predict()
Dự đoán
Cú pháp: model.predict(x_new)
9.6.3.3.3 tensorflow.keras.datasets
9.6.3.3.3.3 tensorflow.keras.datasets.mnist
9.6.3.3.3.3.2
shape
from tensorflow.keras.datasets import mnist
import matplotlib.pyplot as plt

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()

print(x_test.shape)
(10000, 28, 28)
# trong x_test có 10000 ảnh cỡ 28x28
Tải dữ liệu
from tensorflow.keras.datasets import mnist

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()
print(type(x_train), type(y_train))
<class 'numpy.ndarray'> <class 'numpy.ndarray'>
from tensorflow.keras.datasets import mnist
import matplotlib.pyplot as plt

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()

plt.imshow(x_train[0], cmap='gray')
plt.show()
# in ra ảnh viết tay số 5
Thêm chiều kênh
Vì ảnh MNIST là grayscale (1 kênh), cần reshape về dạng (28, 28, 1) nếu dùng CNN
x_train = x_train.reshape(-1, 28, 28, 1)
x_test  = x_test.reshape(-1, 28, 28, 1)

from tensorflow.keras.datasets import mnist
import matplotlib.pyplot as plt

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()
print(x_train.shape)

x_train = x_train.reshape(-1, 28, 28, 1)
print(x_train.shape)
(60000, 28, 28)
(60000, 28, 28, 1)
28.3.2.2.3.4 Thư viện utils
28.3.2.2.3.4.3 Thư viện to_categorical
28.3.2.2.3.4.3.2
One-hot nhãn
from tensorflow.keras.datasets import mnist
from tensorflow.keras.utils import to_categorical

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()

y_train = to_categorical(y_train, num_classes=10)
for i in range(5):
    print(y_train[i])
[0. 0. 0. 0. 0. 1. 0. 0. 0. 0.]
[1. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
[0. 0. 0. 0. 1. 0. 0. 0. 0. 0.]
[0. 1. 0. 0. 0. 0. 0. 0. 0. 0.]
[0. 0. 0. 0. 0. 0. 0. 0. 0. 1.]
28.3.2.2.3.5 Thư viện models
28.3.2.2.3.7 Thư viện losses
MeanSquaredError()
Regression
Cú pháp: tf.keras.losses.MeanSquaredError()
CategoricalCrossentropy()
Classification
Cú pháp: tf.keras.losses.CategoricalCrossentropy()
SparseCategoricalCrossentropy()
Classification
Cú pháp: tf.keras.losses.SparseCategoricalCrossentropy()
28.3.2.2.3.8 Thư viện optimizers
SGD()
Cú pháp: tf.keras.optimizers.SGD(learning_rate)
Adam()
Cú pháp: tf.keras.optimizers.Adam(learning_rate)
RMSprop()
Cú pháp: tf.keras.optimizers.RMSprop(learning_rate)
28.3.2.3.4 Thư viện nn
28.3.2.2.3.1
Relu
Cú pháp: tf.nn.relu
Sigmoid
Cú pháp: tf.nn.sigmoid
Softmax
Cú pháp: tf.nn.softmax
Tanh
Cú pháp: tf.nn.tanh
28.3.2.3.5 Thư viện data
28.3.2.3.6 Thư viện image
28.3.2.3.7 Thư viện io
Ví dụ
Dự đoán ảnh số viết tay
import tensorflow as tf
from tensorflow.keras import layers, models

# Tải dữ liệu
(X_train, y_train), (X_test, y_test) = tf.keras.datasets.mnist.load_data()

# Chuẩn hóa và reshape lại ảnh
X_train = X_train.reshape(-1, 28, 28, 1) / 255.0
X_test = X_test.reshape(-1, 28, 28, 1) / 255.0

# Xây dựng mô hình CNN
model = models.Sequential([
    layers.Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)),
    layers.MaxPooling2D((2, 2)),
    layers.Conv2D(64, (3, 3), activation='relu'),
    layers.MaxPooling2D((2, 2)),
    layers.Flatten(),
    layers.Dense(64, activation='relu'),
    layers.Dense(10, activation='softmax')
])

# Compile mô hình
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# Huấn luyện mô hình
model.fit(X_train, y_train, epochs=5, validation_data=(X_test, y_test))

# Đánh giá
test_loss, test_acc = model.evaluate(X_test, y_test)
print(f'Độ chính xác trên tập test: {test_acc:.2f}')
2025-06-01 15:22:34.288707: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX AVX2
To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.
Epoch 1/5
1875/1875 [==============================] - 15s 8ms/step - loss: 0.1388 - accuracy: 0.9579 - val_loss: 0.0522 - val_accuracy: 0.9829
Epoch 2/5
1875/1875 [==============================] - 15s 8ms/step - loss: 0.0461 - accuracy: 0.9859 - val_loss: 0.0290 - val_accuracy: 0.9900
Epoch 3/5
1875/1875 [==============================] - 17s 9ms/step - loss: 0.0315 - accuracy: 0.9903 - val_loss: 0.0364 - val_accuracy: 0.9877
Epoch 4/5
1875/1875 [==============================] - 16s 9ms/step - loss: 0.0236 - accuracy: 0.9921 - val_loss: 0.0277 - val_accuracy: 0.9911
Epoch 5/5
1875/1875 [==============================] - 16s 9ms/step - loss: 0.0180 - accuracy: 0.9941 - val_loss: 0.0311 - val_accuracy: 0.9905
313/313 [==============================] - 1s 3ms/step - loss: 0.0311 - accuracy: 0.9905
