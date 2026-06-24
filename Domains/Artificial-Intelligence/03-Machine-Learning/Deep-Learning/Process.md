- [Introduction](#introduction)
---
# Introduction
**So sánh ML truyền thống và Deep Learning**
```bash
Machine Learning truyền thống:
    Con người phải tự nghĩ xem dữ liệu có đặc điểm gì quan trọng

Deep Learning:
    Chỉ cần đưa dữ liệu thô vào.
    
    Mạng neural sẽ tự khám phá các đặc điểm quan trọng thông qua nhiều tầng ẩn và dùng chúng để dự đoán

Ví dụ nhận diện chữ số viết tay:
    Ảnh: 8
    
    ML:
        Người lập trình sẽ tự tính:
            - Số vòng tròn trong ảnh
            - Chiều cao
            - Chiều rộng
            - Tỉ lệ nét
            - Số điểm giao nhau
        
        Rồi đưa các đặc trưng đó vào mô hình.
            Ảnh
             ↓
            Con người trích xuất feature
             ↓
            Mô hình học
             ↓
            Kết quả
    => Con người phải tự nghĩ xem đặc trưng nào quan trọng.

    Deep Learning
        Deep Learning bỏ bước đó.
        
        Thay vì:
            Con người tìm feature
        thì:
            Mạng neural tự tìm feature

        Sơ đồ:
        Ảnh
         ↓
        Neural Network
         ↓
        Kết quả
```
**Nếu Deep Learning tự học đặc trưng được thì dùng Deep Learning cho mọi bài toán luôn chứ?**
```bash
Thực tế không phải vậy.

Deep Learning không phải lúc nào cũng tốt hơn
    Deep Learning rất mạnh, nhưng phải trả giá bằng:
        - Cần nhiều dữ liệu hơn
        - Cần nhiều tài nguyên tính toán hơn
        - Huấn luyện lâu hơn
        - Khó giải thích hơn


Trong khi nhiều bài toán thực tế:
    - Dữ liệu ít
    - Dữ liệu dạng bảng (Excel)
    => thì ML truyền thống thường thắng hoặc ngang ngửa DL.

Ví dụ dự đoán giá nhà
    Dữ liệu:
        | Diện tích | Số phòng | Tuổi nhà | Giá  |
        | --------- | -------- | -------- | ---- |
        | 80        | 2        | 5        | 3 tỷ |
        | 120       | 4        | 2        | 5 tỷ |

    Ta đã có sẵn đặc trưng rất rõ ràng:
        - Diện tích
        - Số phòng
        - Tuổi nhà
        - Không có gì để "tự học" thêm nhiều.
    Dùng:
        - Linear Regression
        - Random Forest
        - XGBoost
    => thường rất mạnh.

    Nếu dùng Deep Learning:
        Input
        ↓
        50 lớp
        ↓
        100 lớp
        ↓
        Output
    thì:
        - Chậm hơn
        - Khó tune hơn
        - Kết quả có khi còn kém hơn

Deep Learning phát huy khi dữ liệu quá phức tạp
    Ví dụ ảnh mèo. 
        Input: Ảnh 224×224×3
            Số pixel: 150,528 giá trị
        
        Bạn không thể ngồi thiết kế:
        - tai mèo
        - mắt mèo
        - ria mèo
        - lông mèo
        cho hàng triệu bức ảnh. => Lúc này DL cực kỳ hữu ích.
```
