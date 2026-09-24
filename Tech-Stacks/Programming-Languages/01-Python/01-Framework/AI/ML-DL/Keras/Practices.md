- [Dự đoán ảnh số viết tay](#dự-đoán-ảnh-số-viết-tay)
- [Tải dữ liệu](#tải-dữ-liệu)
- [Chuẩn hóa và reshape lại ảnh](#chuẩn-hóa-và-reshape-lại-ảnh)
- [Xây dựng mô hình CNN](#xây-dựng-mô-hình-cnn)
- [Compile mô hình](#compile-mô-hình)
- [Huấn luyện mô hình](#huấn-luyện-mô-hình)
- [Đánh giá](#đánh-giá)
---
# Dự đoán ảnh số viết tay
```python
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
```