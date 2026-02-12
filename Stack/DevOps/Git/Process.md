- [git remote](#git-remote)
---
# git remote
```bash
- Dùng để kết nối môt repository git cục bộ (trên máy tính của bạn) với một repository từ xa (trên gitHub). 
- giúp git push và git pull. Khi bạn khởi tạo một repository mới trên máy (git init), nó chưa biết liên kết với nơi nào để push code lên
- Dùng khi bạn đã có sẵn code trên máy và muốn đẩy dự án này lên gitHub.
```
**Syn**
```bash
1. Xem remote hiện tại là gì
    git remote -v
2. git remote add origin https://github.com/thang1707/an_toan_bao_mat_tt.git
3. Khi bạn muốn dùng remote origin nhưng trỏ tới repo mới
git remote set-url origin https://github.com/thang170725/elgamal.git
```
git checkout f62cf8
Quay lại bất kỳ commit nào, quay lại commit có địa chỉ f62cf8

Phần 2: Cấu hình dự án bằng git
git init
    1. Tạo ra một kho lưu trữ repo. Tạo ra thư mục ẩn “.git” chứa tất cả các thông tin cần thiết để git theo dõi các thay đổi của dự án.
    2. Hiểu đơn giản là bất đầu nói với git theo dõi sự thay đổi của dự án.
git init EX1
Git sẽ tạo ra một thư mục EX1 mới và nó sẽ trở thành kho lưu trữ repo
(là nơi để quản lý file)
cd vào thư mục a
git init
Thư mục a sẽ trở thành kho lưu trữ repo
git log
Hiển thị lịch sử các commit.
git log --oneline

git add
    3. Đưa vào khu vực tổ chức staging area. Hiểu đơn giản là nói với git những thay đổi nào muốn lưu lại.
    4. git add chỉ lưu vào vùng nhớ tạm thời không đưa vào lịch sử dự án nên cần phải commit để làm điều này.
git add ReadMe.txt
Lưu lại những thay đổi trong file ReadMe.txt
git add .
Lưu lại tất cả
git commit –m “them file”
Một đơn vị làm việc, đưa vào kho lưu trữ repository với nội dung gợi nhớ là them file.
git diff
So sánh với commit cuối cùng, giữa nội dung cũ và mới.
git diff
Xem xem nội dung đã thay đổi với lần commit gần nhất hay chưa
git diff name.txt
Xem xem nội dung đã thay đổi với lần commit gần nhất hay chưa, tại file name.txt
remote repository (kho lưu trữ từ xa)
git init –-bare CentralRepo
Tạo một central repo hay là remote repo.

git remote remove origin
Khi bạn muốn xóa rồi thêm lại remote origin