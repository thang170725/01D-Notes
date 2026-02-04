tensorflow
10.1 Kiến thức cơ sở
    • Tensorflow là một thư viện mã nguồn mở của google dùng để xây dựng và huấn luyện mô hình học máy (ML) và học sâu (DL). Hỗ trợ chạy trên cả CPU, GPU, TPU.
    • Rất mạnh mẽ, được dùng trong thực tế để xây dựng AI như nhận diện ảnh, xử lý ngôn ngữ, dự đoán chuỗi, …
Tensorflow làm gì trong thực tế
Trong thực tế nếu làm việc về xử lý hình ảnh thì ưu tiên chọn tensorflow.
10.2
__version__
Để kiểm tra phiên bản.
constant()
Tạo một tensor là hằng số.
import tensorflow as tf

a = tf.constant([[1,2], [3,4]])
print(a)
tf.Tensor(
[[1 2]
 [3 4]], shape=(2, 2), dtype=int32)
add()
Cộng 2 tensor.
import tensorflow as tf

a = tf.constant([[1,2], [3,4]])
b = tf.constant([[5,6], [7,8]])
sum = tf.add(a,b)
print(sum)
tf.Tensor(
[[ 6  8]
 [10 12]], shape=(2, 2), dtype=int32)
matmul()
Để nhân ma trận.
import tensorflow as tf

a = tf.constant([[1,2], [3,4]])
b = tf.constant([[5,6], [7,8]])
matrix = tf.matmul(a,b)
print(matrix)
tf.Tensor(
[[19 22]
 [43 50]], shape=(2, 2), dtype=int32)
random.uniform()
Tạo một tensor ngẫu nhiên.
import tensorflow as tf

tens = tf.random.uniform([2,2], minval=0, maxval=10, dtype=tf.int32)
print(tens)
tf.Tensor(
[[5 7]
 [1 0]], shape=(2, 2), dtype=int32)
