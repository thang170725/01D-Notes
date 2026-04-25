- [git branch](#git-branch)
---
# git branch
**Ex**
```bash
1. git branch -m master main # Đổi tên nhánh hiện tại từ master -> main.

Lấy code từ 1 nhánh về máy
    1. git checkout khue 
        1. Tạo nhánh khue trên máy bạn
        2. kết nối với nhánh khue trên gitHub
        3. chuyển bạn sang nhánh khue
        4. Tự động lấy code mới nhất từ nhánh khue
    2. git pull origin khue - cập nhật code mới nhất từ nhánh khue
Push từ 1 nhánh lên gitHub
    1. git add .
    2. git commit -m "update tính năng X"
    3. git push origin khue - Nếu gitHub chưa có nhánh Khue → nó sẽ tạo nhánh khue, nếu đã có, nó cập nhật nhánh đó.
commgit push –set-upstream origin nhanh_1
Push lên central repo bằng nhanh_1 khoong phải là nhánh chính
Phần 5: Làm việc với gitHub
Cách clone dự án từ gitHub về máy
    1. Sử dụng git clone
    2. Sử dụng git pull
Đưa code lên gitHub trống
Khi repo gitHub rỗng ta không thể dùng clone là phải dùng:
    1. cd ~/projects/thuc_tap_co_so_nganh/thoi_khoa_bieu (vào thư mục code)
    2. git init
    3. git remote add origin https://github.com/thang170725/thuc_tap_co_so_nganh.git (thêm remote)
git remote set-url origin https://github.com/thang170725/thuc_tap_co_so_nganh.git (nếu dòng trên lỗi)
    4. git add .
    5. git commit -m “first commit”
    6. git branch -M main (đổi tên nhánh chính nếu muốn)
    7. git push -u origin maingit rebase
Tái cơ sở cho một nhánh
Git rebase –continue
Git rebase –skip
git branch –d <B>
Dùng để xóa nhánh B
Git reset –soft <commit id>
Di chuyển head về vị triis commit trạng thái của stage và tất cả sử thay đổi của file được giữ nguyên
Git reset <commit id>
Di chuyển head về vị trí commiit reset vẫn giữ tất cả thay đổi của file, nhưng loại bỏ các thay đổi stage
Git reset –hard <commit id>
Di chuyển con trỏ head về vị trí commit reset và loại bỏ tất cả sử thay đổi của file
Git revert <commit id>
Quay lại commit trước đây
bỏ qua file không cần giám sát
touch .gitignore
tạo ra file .gitignore
cat .gitignore
hiển thị dữ liệu trong file ra màn hình
echo “2/” >> .gitignore
bỏ qua giám sát các file ở folder 2
Xử lý xung đột trong git – Merge Conflict 




Diff file1 file2 : tìm kiếm sự khác biệt giữa file1 và file2
Repository : kho lưu trữ
Commit : một đơn vị làm việc
Branch : nhánh
Main/ master : tên của repo chính
Merge/ rebase : kết hợp 2 nhánh
Develop : tên của nhánh, lập trình viên
Git –-help : hiển thị ra các câu lệnh hướng dẫn




git checkout
Chuyển đổi từ nhánh này sang nhánh nhanh_1.
Cú pháp:
    1. git checkout -b cong origin/cong (tạo nhánh local mới từ nhánh gitHub)
    2. git checkout nhanh_1
git branch
Xem nhánh đang làm việc.
Cú pháp:
    1. git branch -r (Kiểm tra xem nhánh của họ đã có trên remote chưa)
    2. git branch -l
    3. git branch
    4. git branch nhanh_1 (Tạo ra một nhánh mới có tên là nhanh_1)
git fetch
Lấy các thông tin về commit mới từ central, kiểm tra sự thay đổi.
Cú pháp:
    1. git fetch origin (Lệnh này giúp Git cập nhật tất cả thông tin mới từ GitHub bao gồm nhánh mới của bạn bè)
git status
Hiển thị trạng thái của kho lưu trữ.
git merge B
 Gom nội dung của nhánh B vào nhánh A. Khi gom các nhánh lại với nhau rất dễ bị conflict (xung đột).