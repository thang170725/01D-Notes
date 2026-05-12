- [Directory Structure](#directory-structure)
- [Phân loại dữ liệu](#phân-loại-dữ-liệu)
  - [Structured Data (Dữ liệu có cấu trúc)](#structured-data-dữ-liệu-có-cấu-trúc)
  - [Semi-structured Data (Dữ liệu bán cấu trúc)](#semi-structured-data-dữ-liệu-bán-cấu-trúc)
  - [Unstructured Data (Dữ liệu phi cấu trúc)](#unstructured-data-dữ-liệu-phi-cấu-trúc)
- [Format Data (Định dạng file dữ liệu)](#format-data-định-dạng-file-dữ-liệu)
  - [CSV](#csv)
---
# Directory Structure
```bash
01-Data-Preprocessing/      # mình dùng thư mục này để tiền xử lý dữ liệu
├── 01_EDA.md               # mình dùng thư mục này để phân tích dữ liệu trước khi đi vào xử lý
├── Cleaning_Data.md   # mình dùng file này để làm sách dữ liệu 
├── Feature_Scaling.md           # mình dùng file này để xem kiến thức về scaling
├── 04_Categorical_Encoding.md      # biến đổi, chuyển đổi
├── 05_Imbalanced_Data.md           # SMOTE, Undersampling, Oversampling
└── 06_Data_Integration_IO.md       # csv-db.md, đọc/ghi dữ liệu từ nhiều nguồn
```
# Phân loại dữ liệu
## Structured Data (Dữ liệu có cấu trúc)
```bash
Là dữ liệu được tổ chức chặt chẽ trong các bảng (hàng và cột). Đây là "đất diễn" chính của Pandas (file CSV, Excel, SQL).
```
## Semi-structured Data (Dữ liệu bán cấu trúc)
```bash
Không nằm trong bảng nhưng có các thẻ (tags) hoặc dấu hiệu để phân biệt các thành phần. Ví dụ: file JSON, XML, HTML.
```
## Unstructured Data (Dữ liệu phi cấu trúc)
```bash
Không có định dạng cố định và chiếm phần lớn dữ liệu thế giới hiện nay. Ví dụ: Văn bản (Text), Hình ảnh, Âm thanh, Video.
```
# Format Data (Định dạng file dữ liệu)
## CSV 
```bash
- 99% dự án AI đều dùng. CSV phù hợp khi:
    + Dataset đã cố định
    + Dữ liệu snapshot theo thời gian
    + Train offline
```
**Vì sao AI people thích CSV?**
```bash
- Không phụ thuộc DB
- Chạy ở laptop, server, cloud đều được
- Dễ debug (mở bằng mắt)
- Re-train lại model cũ ra đúng kết quả
=> Trong research / training chính thức → CSV là CHUẨN
```