- [Lấy code từ 1 nhánh về máy](#lấy-code-từ-1-nhánh-về-máy)
- [Push vào 1 nhánh lên gitHub](#push-vào-1-nhánh-lên-github)
- [Bài tập tình huống](#bài-tập-tình-huống)
  - [Làm quen tạo branch và cộng tác cơ bản](#làm-quen-tạo-branch-và-cộng-tác-cơ-bản)
  - [Hai dev làm song song, branch bị diverged](#hai-dev-làm-song-song-branch-bị-diverged)
---
# Lấy code từ 1 nhánh về máy
```bash
1. git checkout khue 
    1. Tạo nhánh khue trên máy bạn
    2. kết nối với nhánh khue trên gitHub
    3. chuyển bạn sang nhánh khue
    4. Tự động lấy code mới nhất từ nhánh khue
2. git pull origin khue - cập nhật code mới nhất từ nhánh khue
```
# Push vào 1 nhánh lên gitHub
```bash
1. git add .
2. git commit -m "update tính năng X"
3. git push origin khue # Nếu gitHub chưa có nhánh Khue → nó sẽ tạo nhánh khue, nếu đã có, nó cập nhật nhánh đó.
```
# Bài tập tình huống
## Làm quen tạo branch và cộng tác cơ bản
```bash
- Mục tiêu học:
    + Tạo branch mới
    + Push branch lên GitHub
    + Dev khác lấy branch về và xem được
    + Merge branch vào main
- Bối cảnh
    + Repo hiện có:
        - main
            + 3 thư mục:
                - dev1/
                - dev2/
                - dev3/
    + Giả sử: Bạn mở 3 terminal đại diện cho 3 dev.
```
**Nhiệm vụ**
```bash
Dev1
1. Đảm bảo đang ở main mới nhất:
    1. git checkout main
    2. git pull origin main
2. Tạo branch feature mới:
    - git checkout -b feature/login
3. Trong dev1/ tạo file:
    - login.txt
    - Nội dung: Login feature by dev1
4. Commit:
    1. git add .
    2. git commit -m "Add login feature"
5. Push branch lên GitHub:
    - git push -u origin feature/login

Dev2
1. Không được tạo branch mới.
2. Kiểm tra có thấy branch Dev1 chưa:
    1. git fetch origin
    2. git branch -r
3. Lấy branch đó về local:
    - git checkout -b feature/login origin/feature/login
4. Sửa tiếp file login.txt, thêm dòng:
    - Reviewed by dev2
5. Commit và push:
    1. git add .
    2. git commit -m "Review login feature"
    3. git push

Dev1
1. Lấy update mới từ Dev2:
    - git pull
2. Quay về main:
    - git checkout main
3. Merge feature vào main:
    - git merge feature/login
4. Push:
    - git push
```
## Hai dev làm song song, branch bị diverged
```bash
Mục tiêu học
Hiểu:
    - branch bị diverged là gì
    - pull bị báo phải merge/rebase
    - xử lý merge commit
    - đọc graph commit
    - Đây là thứ đi làm gặp suốt.
Bối cảnh
    - Hiện main sạch sau bài 1.
    - Giả sử hai dev cùng sửa một feature.
    - Ta tạo branch mới:
    - feature/profile
```
```bash
Nhiệm vụ
Dev1

Từ main:

git checkout main
git pull origin main
git checkout -b feature/profile

Tạo file:

dev1/profile.txt

nội dung:

Create profile page

Commit:

git add .
git commit -m "dev1 create profile page"

Push:

git push -u origin feature/profile
Dev2

Lấy branch về:

git fetch
git checkout -b feature/profile origin/feature/profile

Thêm vào cuối file:

Add avatar upload

Commit:

git add .
git commit -m "dev2 add avatar upload"
git push
Quay lại Dev1 (rất quan trọng)

Không pull trước.

Thêm tiếp vào file:

Add profile bio

Commit:

git add .
git commit -m "dev1 add bio"

Giờ thử push:

git push

Phải bị reject kiểu:

rejected
fetch first

Đây chính là diverged.

Remote có commit Dev2
Local có commit Dev1

Hai lịch sử tách nhau.

Xử lý

Chạy:

git pull origin feature/profile

Có thể Git hỏi strategy, nếu có:

git pull --no-rebase origin feature/profile

Nó sẽ tạo merge commit.

Push lại:

git push
Kiểm tra
git log --oneline --graph --all
```