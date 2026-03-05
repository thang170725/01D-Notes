psycopg2
Dùng để kết nối Python với CSDL (PostgreSQL).
import psycopg2
import pandas as pd

conn = psycopg2.connect(
    host="localhost",
    database="batdongsan",
    user="postgres",
    password="170725"
)

query = "SELECT * FROM bat_dong_san;"
df = pd.read_sql_query(query, conn)

conn.close()

print(df.head())
5.2.3 Mã hóa
Khi dữ liệu của bạn có có các danh mục được biểu diễn bằng chuỗi, sẽ rất khó sử dụng để đào tạo mô hình học áy thường chỉ chấp nhận dữ liệu bằng số. Nên cần chuyển dữ liệu chữ thành dữ liệu số.
get_dummies()
chuyển categorical data sang one-hot encoding.
Cú pháp: pd.get_dummies(data, prefix=None, prefix_sep='_', dummy_na=False, columns=None, drop_first=False, dtype=None)
    • data: dữ liệu
    • prefix: Tên tiền tố cho các cột mới 
    • prefix_sep: Ký tự nối giữa prefix và giá trị (mặc định: _)
    • columns: Nếu dùng với DataFrame: chọn các cột cần encode 
    • drop_first: Nếu True, sẽ bỏ cột đầu để tránh đa cộng tuyến (multicollinearity) 
    • dummy_na: Nếu True, tạo thêm cột cho NaN 
    • dtype: Kiểu dữ liệu cho các cột kết quả (mặc định là uint8)
import pandas as pd
df = pd.read_csv("./DataSet1.csv")
one_hot = pd.get_dummies(data=df['loai_dat'], prefix="encode")
print(one_hot.to_string())

   encode_chung _cu  encode_khac  encode_khong  encode_so_do
0              True        False         False         False
1              True        False         False         False
2             False        False          True         False
3             False        False         False          True
4             False        False         False          True
5             False         True         False         False
Hiểu rõ hơn về one-hot:
import pandas as pd

df = pd.DataFrame({
    'dia_diem': ['ha_noi', 'hai_phong', "ha_nam", "ninh_binh"]
})
one_hot = pd.get_dummies(data=df, prefix='encode', dtype=int)
print(one_hot)
   encode_ha_nam  encode_ha_noi  encode_hai_phong  encode_ninh_binh
0              0              1                 0                 0
1              0              0                 1                 0
2              1              0                 0                 0
3              0              0                 0                 1
# encode_ha_nam = [1, 0, 0, 0]
# encode_ha_noi = [0,1,0,0]





5.3 Thư viện albumentations
5.3.1 Kiến thức cơ sở
    • Là một thư viện tăng cường dữ liệu ảnh hiệu suất cao, thân thiện với pytorch và tensorflow.
    • Được thiết kế để hoạt động nhanh và hỗ trợ nhiều kĩ thuật augmentation tiên tiến như:
        ◦ RandomCrop, Flip, Rotate, Blur, CLAHE, RandomBrightnessContrast, Cutout, GridDistortion, …
    • Ưu điểm: Rất nhanh (sử dụng OpenCV backend), dễ tích hợp với tensorflow, pytorch. Có hỗ trợ bbox, segmentation mask, và multi-channel images.
Khi nào cần sử dụng Albuntations​?
    1. Dữ liệu huấn luyện quá ít hoặc không đa dạng => giúp tạo thêm dữ liệu giả lập, tăng khả năng tổng quát hóa.
Ví dụ: Bài toán nhận diện khuôn mặt, bạn chỉ có 300 anhe. albumentations có thể tăng thành 3000 ảnh bằng ảnh lật, xoay mờ, thay đổi ánh sáng, ...
    2. Bài toán có độ phức tạp thị giác cao (CV) => giúp mô hình hiểu “bản chất” của ảnh thay vì học thuộc hình dạng cụ thể.
    3. Khi huấn luyện mô hình học sâu (DL) => giúp tránh overfitting, làm mô hình học được các đặc trưng ền vững hơn.
    4. Khi muốn mô hình hoạt động tốt trên dữ liêuj thực tế đa dạng => giúp mô hình không bị sốc khi gặp ảnh thật.
Cài đặt môi trường
pip install albumentations
5.3.2
Compose([])
    • Đây là hàm gộp các bước augmentation lại thành một pipeline.
    • Thứ tự bên trong […] rất quan trọng vì các bước thực hiện theo đúng thứ tự viết ra.
HorizontalFlip()
    • Lật ảnh theo chiều ngang (gương trái-phải)
    • p: Xác suất ảnh sẽ được lật. Ý nghĩa mô phỏng trường đối tượng nawmg bên trái hoặc phải của ảnh
RandomBrightnessContrast()
    • Thay đổi độ sáng (brightness) và tương phản (contrast) ngẫu nhiên
    • p=0.5: xác suất 50% ảnh sẽ được thay đổi. Giúp mô hình học được trong điều kiện ánh sáng khác nhau (sáng trời, trong nhà, bón tối, …)
Rotate()
    • Xoay ảnh theo góc ngẫu nhiên trong khoảng từ -limit đến +limit độ
    • p=0.1: Xác suất 50% ảnh sẽ bị xoay. Mô phỏng trường ảnh bị nghiêng (do người chụp lệnh tay)
Cú pháp: A.rotate(limit=, p=)
Blur()
    • Làm mờ bằng bộ lọc trung bình
    • p=0.3: Chỉ 30% ảnh sẽ bị làm mờ
    • Nếu bạn không truyền blur_limit, mặc định là blur_limit=(3, 3). Mô phỏng ảnh bị rung nhẹ, lấy nét không chuẩn.
RandomCrop()
    • Cắt ngẫu nhiên một vùng kích thước 200x200 từ ảnh gốc
    • height=200, width=200: kích thước vùng cắt
    • p=1.0: luôn luôn thực hiện cắt. Tạo các góc nhìn khác nhau của ảnh, giúp mô hình học tốt hơn khi đối tượng không nằm giữa ảnh
Resize()
    • Resize ảnh về đúng kích thước. Đảm bảo tất cả ảnh có cùng kích thước trước khi đưa và model