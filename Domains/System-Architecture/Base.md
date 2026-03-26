Thành phần,Thông số của bạn,Lưu ý khi cấu hình dự án
OS máy thật,Ubuntu 24.04,"Rất tốt, tương thích hoàn toàn với các Docker Image mới nhất."
CUDA (trong Docker),<= 12.8,"Bạn nên ưu tiên dùng CUDA 11.8 hoặc 12.1 vì đây là 2 bản ổn định nhất, hỗ trợ nhiều thư viện AI nhất hiện nay."
PyTorch / TensorFlow,Tùy chọn,Luôn chọn bản cài đặt có đuôi +cu118 hoặc +cu121 để khớp với CUDA trong Docker.
Docker Version,29.2.1,"Đây là bản cực mới, hỗ trợ đầy đủ các tính năng buildx và GPU tốt."