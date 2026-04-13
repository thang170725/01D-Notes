- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [version](#version)
- [Layers (Nhóm xây dựng Pipeline)](#layers-nhóm-xây-dựng-pipeline)
  - [.input()](#input)
  - [Conv2D()](#conv2d)
  - [MaxPooling2D()](#maxpooling2d)
  - [Flatten()](#flatten)
  - [Dense()](#dense)
  - [Model()](#model)
  - [model.compile()](#modelcompile)
  - [model.fit()](#modelfit)
  - [model.evaluate()](#modelevaluate)
  - [model.predict()](#modelpredict)
- [Datasets (dữ liệu mẫu trong keras)](#datasets-dữ-liệu-mẫu-trong-keras)
  - [keras.datasets.mnist](#kerasdatasetsmnist)
    - [load\_data()](#load_data)
- [Losses](#losses)
  - [MeanSquaredError()](#meansquarederror)
  - [CategoricalCrossentropy()](#categoricalcrossentropy)
  - [SparseCategoricalCrossentropy()](#sparsecategoricalcrossentropy)
- [optimizers](#optimizers)
  - [SGD()](#sgd)
  - [Adam()](#adam)
  - [RMSprop()](#rmsprop)
- [nn](#nn)
  - [Relu](#relu)
  - [Sigmoid](#sigmoid)
  - [Softmax](#softmax)
  - [Tanh](#tanh)
---
# Display (Nhóm cung cấp thông tin)
## version
**Ex**
```python
import keras
print(keras.__version__)
```
# Layers (Nhóm xây dựng Pipeline)
```bash
(input: 784-dimensional vectors)
       ↧
[Dense (64 units, relu activation)]
       ↧
[Dense (64 units, relu activation)]
       ↧
[Dense (10 units, softmax activation)]
       ↧
(output: logits of a probability distribution over 10 classes)
```
## .input()
```bash
- Đĩnh nghĩa dữ liệu đầu vào của mô hình - tức là hình dạng (shape mà model sẽ nhận).
- Input giống như cổng vào của mạng neural:
    + Bạn phải nói cho model biết: dữ liệu có dạng gì?
    + Ví dụ: ảnh, chuỗi, vector số,…
```
**Syn**
```bash 
from keras.layers import Input

input_layer = Input(shape=(...))

- Input:
    + shape=(...) → kích thước của 1 sample (không tính batch)
```
**Ex**
```python
Input(shape=(10,)) #  Mỗi mẫu có 10 đặc trưng (features)
Input(shape=(224, 224, 3)) # cao: 224, rộng: 224, kênh màu (RGB)
Input(shape=(100,)) # Câu có 100 từ (hoặc 100 token)
```
## Conv2D()
```bash
- Dùng để tạo các kernel lấy đặc trưng cho ảnh
```
**Syn** 
```bash
keras.layers.Conv2D(
    filters= , 
    kernel_size= , 
    activation= , 
    input_shape= , 
    padding=, 
    strides)

- Input
    + Filters: Là số lượng bộ lọc để quét ảnh, mối filter sẽ học một đặc trưng khác nhau (đường ngang, đường dọc, đường cong, …). Bạn có thể chọn bất kỳ số nào, (8,16,64,128,…) => số filters càng nhiều, model càng mạnh (học nhiều đặc trưng hơn) nhưng cững tốn RAM, GPU nhiều hợn, dễ quá tải nếu chọn lớn quá.
    + kernel_size: (3,3)
    + activation: thuật toán học
```
## MaxPooling2D()
```bash
Giảm chiều ảnh.
```
**Syn**
```bash
keras.layers.MaxPooling2D(pool_size)

- Input:
    + pool_zize = (2,2), (4,4), …
```
## Flatten()
```bash
Chuyển ma trận thành vector.
```
**Syn**
```bash
keras.layers.Flatten()
```
## Dense()
```bash
Fully-connected layer.
```
**Syn** 
```bash
keras.layers.Dense(<number>, activation=)

- Input:
    + Number: xác định số nút nơ ron, bạn hoàn toàn có thể đổi thành 64,256,512, … miễn là hợp lý và không quá nặng so với dung lượng máy.
```
## Model()
**Ex**
```python
def PipelineCNN():
    inputs = Input(shape=(8, 8, 1))   # ✅ đúng shape

    x = Conv2D(32, (3,3), activation='relu')(inputs)
    x = MaxPool2D(pool_size=(2,2))(x)
    x = Flatten()(x)
    x = Dense(64, activation='relu')(x)
    outputs = Dense(10, activation='softmax')(x)

    model = Model(inputs, outputs)
    return model
```
## model.compile()
```bash
Biên dịch mô hình.
```
**Syn**
```bash
model.compile(optimizer, loss, metrics)

- Input:
    + Optimizer: Đây là thuật toán giúp mô hình cập nhật trọng số để học tốt hơn sau mỗi lần huấn luyên.
    + Loss: Là thước đo sai số giữa dự đoán của mô hình và kết quả thật.
    + Metrics: Dùng để đo lường độ chính xác của mô hình sau mỗi epoch. Accuracy = (số dự đoán đúng)/(tổng số mẫu)
```
## model.fit()
```bash
Huấn luyện
```
**Syn** 
```bash
model.fit(x, y, epochs, bath_size)
```
## model.evaluate()
```bash
Đánh giá
```
**Syn** 
```bash
model.evaluate(x_test, y_test)
```
## model.predict()
```bash
Dự đoán
```
**Syn**
```bash
model.predict(x_new)
```
Embedding()
Dùng trong NLP
Cú pháp: tf.keras.layers.Embedding(input_dim, output_dim)
LSTM()
Dùng trong NLP tuần tự.
Cú pháp: tf.keras.layers.LSTM(units)
GRU()
Dùng trong NLP tuần tự.
Cú pháp: tf.keras.layers.GRU(units)
model
API tùy chỉnh model nâng cao
# Datasets (dữ liệu mẫu trong keras)
## keras.datasets.mnist
### load_data()
**Ex**
```python
from tensorflow.keras.datasets import mnist
import matplotlib.pyplot as plt

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()

print(x_test.shape) # (10000, 28, 28), trong x_test có 10000 ảnh cỡ 28x28
```
**Ex2: Tải dữ liệu**
```python
from tensorflow.keras.datasets import mnist

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()

print(type(x_train), type(y_train)) # <class 'numpy.ndarray'> <class 'numpy.ndarray'>
```
**Ex3: Hiển thị ảnh trong mnist**
```python
from tensorflow.keras.datasets import mnist
import matplotlib.pyplot as plt

# Tải dữ liệu
(x_train, y_train), (x_test, y_test) = mnist.load_data()

plt.imshow(x_train[0], cmap='gray')
plt.show()
```
# Losses
## MeanSquaredError()
## CategoricalCrossentropy()
## SparseCategoricalCrossentropy()
# optimizers
## SGD()
**Syn** 
```bash
keras.optimizers.SGD(learning_rate)
```
## Adam()
**Syn** 
```bash
keras.optimizers.Adam(learning_rate)
```
## RMSprop()
**Syn** 
```bash
keras.optimizers.RMSprop(learning_rate)
```
# nn
## Relu
## Sigmoid
## Softmax
## Tanh