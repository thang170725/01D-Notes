- [git config](#git-config)
- [git clone](#git-clone)
- [git pull](#git-pull)
  - [--no-rebase](#--no-rebase)
- [git push](#git-push)
  - [-u](#-u)
  - [-f \& --force](#-f----force)
  - [--delete](#--delete)
- [git init](#git-init)
- [.gitignore](#gitignore)
- [.git](#git)
- [git reset](#git-reset)
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
# git pull
```bash
- Lấy dữ liệu và hợp nhất (merge) những thay đổi đó vào nhánh hiện tại của bạn. 
- Lệnh này là sự kết hợp của 2 lệnh git fetch (lấy các thay đổi từ kho lưu trữ từ xa) và git merge (hợp nhất các thay đổi vào nhánh hiện tại)
```
**Syn**
```bash
1. pull từ nhánh main
    git pull origin main
```
## --no-rebase
**Ex**
```bash
git pull --no-rebase origin feature/profile

- --no-rebase: Bắt Git dùng merge, không dùng rebase (nghĩa là fetch + merge)
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
## --delete
```bash
git push origin --delete feature/login # xóa branch trên gitHub
```
# git init
```bash
- Dùng để:
    1. Tạo ra một kho lưu trữ repo. Tạo ra thư mục ẩn “.git” chứa tất cả các thông tin cần thiết để git theo dõi các thay đổi của dự án.
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
# .gitignore
**Hạn chế thư mục push lên gitHub**
```bash
~/workspace/lightgbm
├── backend
│   └── dataset
├── docs
├── frontend
└── README.md
```
```bash
Muốn backend/dataset không push lên Git.

Bước 1: đứng ở root project
    - cd ~/workspace/lightgbm
Bước 2: tạo .gitignore
    - touch .gitignore
Bước 3: mở file .gitignore
    1. nano .gitignore
    2.  thêm dòng này: backend/dataset/
    3.  Lưu: Ctrl + O → Enter, Ctrl + X
Bước 4: kiểm tra
    - cat .gitignore
    - phải ra: backend/dataset/
Bước 5: add code
    - git add .
    - dataset sẽ bị bỏ qua.
    - Kiểm tra: git status (sẽ không thấy backend/dataset)
    - .gitignore cho project bạn có thể sau này mở rộng:
        backend/dataset/
        __pycache__/
        *.pyc
        .env
        venv/
```
# .git
**Ex: Xóa .git và init lại từ đầu để xóa toàn bộ lịch sử repo**
```bash
rm -rf .git
git init
git add .
git commit -m "Initial commit"
git remote add origin <repo-url>
git push -f origin main
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