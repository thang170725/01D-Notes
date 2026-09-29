Python
import fasttext

# Cấu hình FastText siêu nhẹ và siêu nhanh cho 80 nhãn
model = fasttext.train_supervised(
    input='train_data.txt',
    
    # 1. TẮT hoặc GIẢM Subword/Character n-gram nếu sợ chậm:
    # Với tiếng Việt đã tokenize (ví dụ: bảo_hiểm_nhân_thọ), từ vựng khá rõ ràng,
    # bạn có thể đặt minn=0, maxn=0 để TẮT HOÀN TOÀN char n-gram (chạy nhanh như Word2Vec).
    minn=0, 
    maxn=0,
    
    # 2. Bật Word N-gram (Cụm từ):
    # Dùng word n-gram = 2 hoặc 3 để bắt các cụm như "thông_báo bồi_thường", "thư_gửi đại_lý"
    wordNgrams=2,
    
    # 3. Dùng Hierarchical Softmax cho tập nhãn lớn (80 nhãn):
    loss='hs',
    
    # 4. Ép kích thước bảng băm nhỏ lại để tiết kiệm RAM/Bộ nhớ:
    bucket=200000,
    
    # Số chiều vector (50-100 là vừa đủ):
    dim=100,
    
    epoch=25,
    lr=0.5
)
Mẹo: Khi đặt minn=0 và maxn=0, FastText quay trở về mô hình Phân loại Word-level truyền thống. Tốc độ dự đoán lúc này rơi vào khoảng 0.5 - 1 millisecond / email trên CPU!
