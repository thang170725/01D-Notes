- [git remote](#git-remote)
- [git add](#git-add)
- [git commit](#git-commit)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [git status (Dùng để xem trạng thái repo hiện tại)](#git-status-dùng-để-xem-trạng-thái-repo-hiện-tại)
  - [git log](#git-log)
  - [git diff](#git-diff)
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
# git add
```bash
- Đưa vào khu vực tổ chức staging area. Hiểu đơn giản là nói với git những thay đổi nào muốn lưu lại.
- git add chỉ lưu vào vùng nhớ tạm thời không đưa vào lịch sử dự án nên cần phải commit để làm điều này.
```
**Ex**
```bash
git add ReadMe.txt # Lưu lại những thay đổi trong file ReadMe.txt
git add . # Lưu lại tất cả
```
# git commit
```bash
Một đơn vị làm việc, đưa vào kho lưu trữ repository với nội dung gợi nhớ là them file.
```
**Ex**
```bash
git commit –m “them file”
```
# Display (Nhóm cung cấp thông tin)
## git status (Dùng để xem trạng thái repo hiện tại)
```bash
- đang ở branch nào
- file nào sửa nhưng chưa stage
- file nào đã stage
- có conflict không
- branch có ahead/behind remote không
```
**Ex**
```bash
Sau:
  git add app.py
  git status
ra:
  Changes to be committed:
    modified: app.py
Nghĩa:
  - file đã vào staging area
  - sẵn sàng commit
```
## git log
```bash
Hiển thị lịch sử các commit.
```
**Syn**
```bash
git log --oneline --graph --all

- --oneline : Rút gọn mỗi commit thành 1 dòng
- --graph   : Vẽ cây branch/merge bằng ASCII
- --all     : xem mọi branch: local branches, remote-tracking branches
```
## git diff
```bash
- So sánh với commit cuối cùng, giữa nội dung cũ và mới.
- Dùng để xem sự khác biệt
```
**Ex1**
```bash
git diff # Xem xem nội dung đã thay đổi với lần commit gần nhất hay chưa
git diff name.txt # Xem xem nội dung đã thay đổi với lần commit gần nhất hay chưa, tại file name.txt
```
**Ex2**
```bash
File cũ: print("hello")
Bạn sửa: print("hello world")

chạy: git diff
  ra:
    -print("hello")
    +print("hello world")
  Ý nghĩa:
  - dòng bị xóa: -
  - dòng thêm: +
  - Quan trọng: git diff
  - so sánh: Working directory vs staging (tức sửa nhưng chưa add)
  - Sau git add. git diff có thể không ra gì. vì đã stage.
```