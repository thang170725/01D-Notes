Chương 2: SQL Sever
Kiểu dữ liệu




Char(n)
Cố định n ký tự
Char(10) nếu điền ‘An’ database vẫn dùng 10


Varchar(n)
Chỉ dùng đúng số ký tự cần
Varchar(10) nếu điều ‘An’ database chỉ dùng 2



Thêm
Thêm dữ liệu 
Cú pháp:
INSERT INTO Users (Username, Password, Email)
VALUES (N'admin', N'123456', N'admin@example.com');
INSERT INTO Users (Username, Password, Email)
VALUES
    (N'user1', N'pass1', N'user1@example.com'),
    (N'user2', N'pass2', N'user2@example.com'),
    (N'user3', N'pass3', N'user3@example.com');
INSERT INTO Users
VALUES (1, N'test', N'1234', N'test@example.com');
Cập nhật
Đổi kiểu dữ liệu cho cột
Cú pháp:
ALTER TABLE TenBang
ALTER COLUMN TenCot KieuDuLieuMoi [NULL | NOT NULL];
ALTER TABLE Users
ALTER COLUMN Username CHAR(50) NOT NULL;
Sửa giá trị hiện có
Ví dụ bảng Users có cột Username đang lưu là "lê đức thắng", bạn muốn đổi thành "thắng".
Cú pháp:
UPDATE Users
SET Username = N'thắng'
WHERE Username = N'lê đức thắng';
WHERE rất quan trọng để chỉ định hàng nào sẽ được cập nhật. Nếu bỏ WHERE, tất cả các dòng trong bảng sẽ bị đổi
Cập nhật cột đang rỗng
UPDATE Users
SET Full_Name = N'lê đức thắng'
WHERE UserID = 1;
UPDATE Users
SET Full_Name = N'lê đức thắng'
WHERE Full_Name IS NULL
  AND UserID = 1;

Xem n hàng trong bảng
Cú pháp:
SELECT COUNT(*)
FROM TenBang;
Xóa hàng trong bảng
Cú pháp:
DELETE FROM TenBang
WHERE dieu_kien;
DELETE FROM UserName
WHERE id = 1;
Xoá bản ghi có id = 1 trong bảng UserName.
DELETE FROM UserName
WHERE username = 'thang';
Thêm cột
Cú pháp:
ALTER TABLE TenBang
ADD TenCot KieuDuLieu [NULL | NOT NULL] [DEFAULT gia_tri];
ALTER TABLE UserName
ADD email NVARCHAR(50) NULL;
ALTER TABLE UserName
ADD age INT, address NVARCHAR(100);
Xóa cột 
Cú pháp:
ALTER TABLE TenBang
DROP COLUMN TenCot;
ALTER TABLE UserName
DROP COLUMN email;
