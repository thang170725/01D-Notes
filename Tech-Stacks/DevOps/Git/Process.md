- [git config](#git-config)
- [git clone](#git-clone)
- [git pull (Lấy dữ liệu \& hợp nhất)](#git-pull-lấy-dữ-liệu--hợp-nhất)
  - [--no-rebase (Bắt Git dùng merge, không dùng rebase (nghĩa là fetch + merge))](#--no-rebase-bắt-git-dùng-merge-không-dùng-rebase-nghĩa-là-fetch--merge)
  - [git config pull (đây là các cách pull cũ)](#git-config-pull-đây-là-các-cách-pull-cũ)
- [git push](#git-push)
  - [-u](#-u)
  - [-f \& --force](#-f----force)
  - [–set-upstream](#set-upstream)
  - [--delete (xóa nhánh trên github)](#--delete-xóa-nhánh-trên-github)
- [git init (Tạo ra một kho lưu trữ repo)](#git-init-tạo-ra-một-kho-lưu-trữ-repo)
- [git reset](#git-reset)
- [git remote (Dùng để kết nối môt repository git cục bộ (trên máy tính của bạn) với một repository từ xa (trên gitHub))](#git-remote-dùng-để-kết-nối-môt-repository-git-cục-bộ-trên-máy-tính-của-bạn-với-một-repository-từ-xa-trên-github)
  - [-v (Xem remote hiện tại là gì)](#-v-xem-remote-hiện-tại-là-gì)
  - [add](#add)
  - [set-url (Khi bạn muốn dùng remote origin nhưng trỏ tới repo mới)](#set-url-khi-bạn-muốn-dùng-remote-origin-nhưng-trỏ-tới-repo-mới)
- [git add](#git-add)
- [git commit](#git-commit)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [git status (Dùng để xem trạng thái repo hiện tại)](#git-status-dùng-để-xem-trạng-thái-repo-hiện-tại)
  - [git log (Hiển thị lịch sử các commit)](#git-log-hiển-thị-lịch-sử-các-commit)
  - [git diff](#git-diff)
- [git reset](#git-reset-1)
  - [–soft](#soft)
  - [–hard (Di chuyển con trỏ head về vị trí commit reset và loại bỏ tất cả sử thay đổi của file)](#hard-di-chuyển-con-trỏ-head-về-vị-trí-commit-reset-và-loại-bỏ-tất-cả-sử-thay-đổi-của-file)
- [Git revert (Quay lại commit trước đây)](#git-revert-quay-lại-commit-trước-đây)
---
# git config
**Syn**
```bash
1. –l (Xem toàn bộ thông tin cấu hình hiện tại)
2. git config –-global user.name “Le Duc Thang“ (Cấu hình tên của người dùng là Le Duc Thang)
3. git config –-global user.email “Le Duc Thang“ (Cấu hình email của người dùng là Le Duc Thang)
4. git config –-local user.name “Le Duc Thang“ (Cấu hình tên của người dùng là Le Duc Thang)
5. git config –-local user.email “Le Duc Thang“ (Cấu hình email của người dùng là Le Duc Thang)
6. Xem thông tin cấu hình 
    - git config –l -–global (Xem thông tin cấu hình của global)
    - git config –l –-local (Xem thông tin cấu hình của local)
    - git config --list                              
```
# git clone 
```bash
Lệnh này giúp bạn sao chép toàn bộ mã nguồn, lịch sử thay đổi, nhánh, commit, và tất cả các file trong dự án về máy tính để làm việc trực tiếp.
```
**Syn**
```bash
1. Sao chép ma nguồn từ gitHub vào thư mục dev1
    git clone https://github.com/thang1707/lesson1.git dev1
2. git clone https://github.com/thang1707/lesson1.git .
2. clone nhánh cụ thể về máy tính
    git clone --branch khue --single-branch https://github.com/thang170725/elgamal.git
```
# git pull (Lấy dữ liệu & hợp nhất)
```bash
Lệnh này là sự kết hợp của 2 lệnh:
  - git fetch (lấy các thay đổi từ kho lưu trữ từ xa)
  - git merge (hợp nhất các thay đổi vào nhánh hiện tại)
```
**Ex: pull từ nhánh main**
```bash
git pull origin main
```
## --no-rebase (Bắt Git dùng merge, không dùng rebase (nghĩa là fetch + merge))
**Ex**
```bash
git pull --no-rebase origin feature/profile 
```
## git config pull (đây là các cách pull cũ)
**Syn**
```bash
git config pull.rebase false # tương đương với git pull --no-rebase
git config pull.rebase true # git pull --rebase
git config pull.ff only # git pull --ff-only
```
# git push
## -u
**Ex**
```bash
git push -u origin feature/login

- origin    : Là remote repo (thường là GitHub).
    + origin chỉ là nickname, có thể đổi tên khác được.
- feature/login : Branch local bạn muốn push lên remote.
- -u    : -u = --set-upstream
    + Nó thiết lập branch local theo dõi branch remote tương ứng:
    + feature/login  ---> origin/feature/login
    + Sau đó Git nhớ:
        - pull từ đâu
        - push tới đâu

# Lần đầu: git push -u origin feature/login
# Các lần sau chỉ cần: git push hoặc git pull
# không cần ghi lại origin + branch.
```
**Nếu không có -u**
```bash
git push origin feature/login

# vẫn push được. Nhưng lần sau: git push có thể Git báo: no upstream branch vì chưa liên kết tracking branch.
```
**Có bỏ origin được không?**
```bash
Lần đầu thường không nên bỏ.

git push -u origin feature/login # rõ ràng nhất.

# Sau khi set upstream rồi:
# Có thể: git push không cần origin.
# Tư duy Lần đầu: git push -u origin feature/login = "Đẩy branch này lên GitHub và nhớ đây là branch remote của tôi."
# Sau đó: git pushgit pull là đủ.
```
## -f & --force
**Ex**
```bash
git push -f origin main # force push đè GitHub
```
## –set-upstream 
## --delete (xóa nhánh trên github)
```bash
git push origin --delete feature/login # xóa branch trên gitHub
```
# git init (Tạo ra một kho lưu trữ repo)
```bash
- Dùng để:
    1. Tạo ra thư mục ẩn “.git” chứa tất cả các thông tin cần thiết để git theo dõi các thay đổi của dự án.
    2. Hiểu đơn giản là bất đầu nói với git theo dõi sự thay đổi của dự án.
```
**Ex1**
```bash
git init EX1 # Git sẽ tạo ra một thư mục EX1 mới và nó sẽ trở thành kho lưu trữ repo (là nơi để quản lý file)
```
**Ex2**
```bash
1. cd vào thư mục a
2. git init # Thư mục a sẽ trở thành kho lưu trữ repo
```

# git reset 
```bash
- dùng để đưa HEAD / branch / staging area quay về commit cũ hoặc trạng thái khác.
```
**Ex**
```bash
Bạn có 3 commit:
A --- B --- C   (main)
Hiện tại đang ở commit C.
Nếu chạy:
git reset --hard B
thì branch main sẽ quay lại:
A --- B   (main)
Commit C coi như bị bỏ khỏi branch hiện tại.
```
**Ex2**
```bash
Bạn code:
git add .git commit -m "bug code"
Sau đó phát hiện commit này phá project.
Bạn muốn quay về commit trước:
git reset --hard HEAD~1
Ý nghĩa:
HEAD = commit hiện tại
HEAD~1 = commit trước đó
Kết quả:
commit lỗi biến mất
code trong folder cũng quay lại như trước
```
**Ex3**
```bash
Bạn đang ở nhánh:
main  -> code mớithang -> code cũ
Bạn chạy:
git checkout thang
git reset --hard main
Nghĩa là: "hãy làm cho nhánh thang giống y hệt commit hiện tại của main"
Sau đó: 
main  -> A B C
thang -> A B C
Code cũ trên thang biến mất.
```
# git remote (Dùng để kết nối môt repository git cục bộ (trên máy tính của bạn) với một repository từ xa (trên gitHub))
```bash
- giúp git push và git pull. Khi bạn khởi tạo một repository mới trên máy (git init), nó chưa biết liên kết với nơi nào để push code lên
- Dùng khi bạn đã có sẵn code trên máy và muốn đẩy dự án này lên gitHub.
```
## -v (Xem remote hiện tại là gì)
**Syn**
```bash
git remote -v
```
## add
**Syn**
```bash
git remote add origin https://github.com/thang1707/an_toan_bao_mat_tt.git
```
## set-url (Khi bạn muốn dùng remote origin nhưng trỏ tới repo mới)
**Syn**
```bash
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
## git log (Hiển thị lịch sử các commit)
**Syn**
```bash
git log --oneline --graph --all

- --oneline : Rút gọn mỗi commit thành 1 dòng
- --graph   : Vẽ cây branch/merge bằng ASCII
- --all     : xem mọi branch: local branches, remote-tracking branches
```
**Cách thoát khỏi git log**
```bash
Để thoát, chỉ cần nhấn: q # (q = quit)
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
# git reset 
## –soft 
## –hard (Di chuyển con trỏ head về vị trí commit reset và loại bỏ tất cả sử thay đổi của file)
# Git revert (Quay lại commit trước đây)
