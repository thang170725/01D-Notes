- [Tạo một repository trên gitHub](#tạo-một-repository-trên-github)
- [Đưa code lên gitHub trống](#đưa-code-lên-github-trống)
---
# Tạo một repository trên gitHub
```bash
- Repository là một vùng lưu trữ các folder, file được gửi từ máy tính cá nhân lên gitHub.
- Khi tạo repository trên gitHub xong ta cần kết nối và đưa code lên repository lần đầu tiên.
```
**Step**
```bash
1. echo "# tri_tue_nhan_tao" >> README.md
2. git init
3. git add README.md
4. git commit -m "first commit"
5. git branch -M main
6. git remote add origin https://github.com/thang170725/tri_tue_nhan_tao.git
7. git push -u origin main
Lưu ý: Cần sử dụng git config trước để tạo tên đăng nhập
```
# Đưa code lên gitHub trống
```bash
Khi repo gitHub rỗng ta không thể dùng clone, phải dùng:
```
```bash
1. cd ~/projects/thuc_tap_co_so_nganh/thoi_khoa_bieu (vào thư mục code)
2. git init
3. Tạo remote trỏ tới url github
    - git remote add origin https://github.com/thang170725/thuc_tap_co_so_nganh.git (thêm remote)
    - git remote set-url origin https://github.com/thang170725/thuc_tap_co_so_nganh.git (nếu dòng trên lỗi)
4. git add .
5. git commit -m “first commit”
6. git branch -M main (đổi tên nhánh chính nếu muốn)
7. git push -u origin maingit rebase
```
tôi muốn test thử chức năng quay lại commit cũ, với các trường hợp đã thêm sửa xóa thì làm như nào, tôi đang học git
Đây là cách học Git rất hiệu quả. Bạn nên tạo một repo thử nghiệm và thực hành đầy đủ các tình huống. Mình gợi ý kịch bản sau.

Bước 1: Tạo repo
mkdir git-practice
cd git-practice

git init

Tạo 3 file:

a.txt
b.txt
c.txt

Nội dung:

a.txt
Hello A
b.txt
Hello B
c.txt
Hello C

Commit đầu tiên:

git add .
git commit -m "Initial commit"
Bước 2: Tạo commit thứ hai
Sửa a.txt
Hello A
Version 2
Xóa b.txt
Thêm d.txt
Hello D

Commit:

git add .
git commit -m "Second commit"

Lúc này:

Commit 2
├── a.txt (đã sửa)
├── c.txt
└── d.txt (mới)

Commit 1
├── a.txt
├── b.txt
└── c.txt
Bước 3: Tạo commit thứ ba
Sửa c.txt
Hello C
Version 3
Thêm e.txt

Commit:

git add .
git commit -m "Third commit"
Bây giờ bạn có thể thực hành
1. Xem lịch sử
git log --oneline

Ví dụ

a1b2c3 Third commit
d4e5f6 Second commit
g7h8i9 Initial commit
2. Quay về commit cũ (không phá lịch sử)
git checkout g7h8i9

hoặc

git switch --detach g7h8i9

Bạn sẽ thấy:

a.txt
b.txt
c.txt

Không còn

d.txt
e.txt

Đây chỉ là xem lại lịch sử.

Quay về mới nhất:

git switch main
3. Reset
Soft
git reset --soft HEAD~1

Kết quả

Commit thứ 3 biến mất

Các thay đổi vẫn nằm trong Staging Area
Mixed (mặc định)
git reset HEAD~1

Kết quả

Commit biến mất

File vẫn còn

Chưa được git add
Hard
git reset --hard HEAD~1

Kết quả

Commit biến mất

File quay lại trạng thái commit trước

Mọi thay đổi chưa commit cũng mất
4. Restore một file

Ví dụ sửa

a.txt

rồi

git restore a.txt

File trở về đúng nội dung của commit gần nhất.

5. Khôi phục file đã xóa

Ví dụ

rm b.txt

Git báo

deleted: b.txt

Khôi phục

git restore b.txt
6. Khôi phục file đã commit trước đó

Ví dụ đang ở commit 3 nhưng muốn lấy b.txt từ commit 1

git restore --source=<commit_hash> b.txt

Ví dụ

git restore --source=g7h8i9 b.txt
7. Revert

Đây là cách rất hay khi làm việc nhóm.

git revert HEAD

Git sẽ tạo thêm một commit mới để hoàn tác commit gần nhất, thay vì xóa lịch sử.

8. Xem sự khác nhau

So với commit trước

git diff HEAD~1

So với commit đầu

git diff g7h8i9
Mình khuyên bạn thực hành theo đúng thứ tự này
Tạo 3 commit.
Thử thêm file.
Thử xóa file.
Thử sửa file.
Dùng git checkout (hoặc git switch --detach) để xem commit cũ.
Dùng git restore để khôi phục file.
Dùng git reset --soft.
Dùng git reset.
Dùng git reset --hard.
Dùng git revert.

Sau khi làm hết các bước trên, bạn sẽ hiểu gần như toàn bộ các thao tác Git cơ bản liên quan đến việc quay lại commit cũ và hoàn tác thay đổi.

Lưu ý: Hãy thực hành trên một repo thử nghiệm như trên. Đừng dùng git reset --hard trên dự án thật khi còn thay đổi chưa được commit, vì lệnh này sẽ xóa các thay đổi đó khỏi thư mục làm việc.