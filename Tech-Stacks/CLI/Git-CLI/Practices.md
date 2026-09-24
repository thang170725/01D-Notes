- [Tạo một repository trên gitHub (dùng khi đã có code rồi và muốn tạo repo trên github)](#tạo-một-repository-trên-github-dùng-khi-đã-có-code-rồi-và-muốn-tạo-repo-trên-github)
- [quay lại commit cũ khi đã thêm sửa xóa repo](#quay-lại-commit-cũ-khi-đã-thêm-sửa-xóa-repo)
- [mô phỏng lại quá trình làm team với git](#mô-phỏng-lại-quá-trình-làm-team-với-git)
- [cách khắc phục khi lỡ commit key bị lỗi push nhưng khi fix xong thì lại không push lên được nữa](#cách-khắc-phục-khi-lỡ-commit-key-bị-lỗi-push-nhưng-khi-fix-xong-thì-lại-không-push-lên-được-nữa)
- [sửa .env](#sửa-env)
---
# Tạo một repository trên gitHub (dùng khi đã có code rồi và muốn tạo repo trên github)
**Step: Các bước hướng dẫn**
```bash
1. echo "# tri_tue_nhan_tao" >> README.md
2. git init
3. git add README.md
4. git commit -m "first commit"
5. git branch -M main
6. git remote add origin https://github.com/thang170725/tri_tue_nhan_tao.git # git remote set-url origin .... nếu add origin bị lỗi
7. git push -u origin main

Lưu ý: Cần sử dụng git config trước để tạo tên đăng nhập
```
# quay lại commit cũ khi đã thêm sửa xóa repo
**Bước 1: Tạo repo**
```bash
1. mkdir git-practice # tạo thư mục test
2. cd git-practice # đi vào thư mục
3. git init # tạo git repo
4. Tạo 3 file:
    - a.txt có nội dung "Hello A"
    - b.txt có nội dung "Hello B"
    - c.txt có nội dung "Hello C"
5. Commit đầu tiên:
    - git add .
    - git commit -m "Initial commit"
```
**Bước 2: Tạo commit thứ hai**
```bash
1. Sửa a.txt: Hello A -> Version 2
2. Xóa b.txt
3. Thêm d.txt có nội dung là "Hello D"
4. Commit:
    - git add .
    - git commit -m "Second commit"

Lúc này:
    Commit 2
    ├── a.txt (đã sửa)
    ├── c.txt
    └── d.txt (mới)

    Commit 1
    ├── a.txt
    ├── b.txt
    └── c.txt
```
**Bước 3: Tạo commit thứ ba**
```bash
1. Sửa c.txt: Hello C -> Version 3
2. Thêm e.txt
3. Commit:
    - git add .
    - git commit -m "Third commit"
```
**Bây giờ bạn có thể thực hành**
**1. Xem lịch sử**
```bash
git log --oneline
# a1b2c3 Third commit
# d4e5f6 Second commit
# g7h8i9 Initial commit
```
**2. Quay về commit cũ (không phá lịch sử)**
```bash
git checkout g7h8i9 hoặc git switch --detach g7h8i9
    Bạn sẽ thấy:
        a.txt
        b.txt
        c.txt

    Không còn
        d.txt
        e.txt

Đây chỉ là xem lại lịch sử.

Quay về mới nhất: git switch main
```
**3. Reset**
```bash
git reset --soft HEAD~1 # Kết quả: Commit thứ 3 biến mất Các thay đổi vẫn nằm trong Staging Area

git reset HEAD~1 # Kết quả Commit biến mất File vẫn còn. Chưa được git add

git reset --hard HEAD~1 # Kết quả Commit biến mất. File quay lại trạng thái commit trước. Mọi thay đổi chưa commit cũng mất
```
**4. Restore một file**
```bash
Ví dụ:
    sửa: a.txt
        rồi: git restore a.txt
-> File trở về đúng nội dung của commit gần nhất.
```
**5. Khôi phục file đã xóa**
```bash
rm b.txt
    Git báo: deleted: b.txt

Khôi phục: git restore b.txt
```
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

# mô phỏng lại quá trình làm team với git
```bash
Ví dụ mô phỏng một team 3 người:
                main
                 │
      ┌──────────┴──────────┐
      │                     │
  feature/login        feature/payment
      │                     │
   commit A               commit C
      │                     │
      └────── merge ────────┘
                 │
              conflict
                 │
              resolve

Ta sẽ cố tình tạo:
    - Branch
    - Nhiều developer cùng sửa một file
    - Merge bình thường
    - Merge conflict
    - Resolve conflict
    - Commit nhầm
    - git restore
    - git reset
    - git revert
    - Push/pull mô phỏng remote
    - Tạo tình huống non-fast-forward
    - Rebase để hiểu tại sao team hay dùng nó

Quan trọng: làm trên một project test riêng, đừng làm trên project thật.
```
**1. Tạo project mô phỏng**
```bash
1. cd D:\workspace
2. mkdir git_team_simulation
3. cd git_team_simulation
4. git init
5. Kiểm tra:
    - git status
    - git branch
6. Tạo file:
    - echo "# Git Team Simulation" > README.md
    - echo "print('Hello')" > app.py
7. Commit:
    - git add .
    - git commit -m "Initial project"
8. Kiểm tra:
    - git log --oneline --graph --all
    - git branch # Nếu là master: git branch -M main
```
**2. Mô phỏng Developer A**
```bash
Giả sử Developer A nhận task: Làm chức năng login.

1. Tạo branch: git switch -c feature/login
2. Kiểm tra: git branch 
# Bạn sẽ thấy:
# * feature/login
#   main
3. Sửa app.py thành:
def login():
    print("Login by Developer A")
4. Commit:
    - git add app.py
    - git commit -m "Add login feature"
# Lúc này lịch sử:
# main
#  │
#  ● Initial project
#  │
#  ● Add login feature
#        ↑
#  feature/login

# main vẫn ở commit cũ.
```
**3. Developer B làm việc song song**
```bash
1. Quay về main: git switch main
2. Tạo branch của Developer B: git switch -c feature/payment
3. Sửa app.py:
def payment():
    print("Payment by Developer B")
4. Commit:
    - git add app.py
    - git commit -m "Add payment feature"
# Bây giờ Git graph:
#                     ● Add login
#                    /
# ● Initial project
#                    \
#                     ● Add payment
-> Đây chính là tình huống hai developer tách ra từ cùng một commit.
```
**4. Merge Developer A**
```bash
1. Quay về main: git switch main
2. Merge: git merge feature/login
# Nếu thành công:
# main
#  │
#  ● Add login
3. Kiểm tra: git log --oneline --graph --all
```
**5. Bây giờ chơi trò nguy hiểm 😈**
```bash
1. git switch main
2. git merge feature/payment
Bạn rất có thể sẽ gặp conflict.

Git có thể báo:

CONFLICT (content): Merge conflict in app.py
Automatic merge failed; fix conflicts and then commit the result.

🔥 Đây chính là thứ mình muốn bạn tập.

6. Mở app.py

Bạn sẽ thấy đại loại:

<<<<<<< HEAD
def login():
    print("Login by Developer A")
=======
def payment():
    print("Payment by Developer B")
>>>>>>> feature/payment

print("Hello")

Git đang nói:

<<<<<<< HEAD
        ↓
Code hiện tại của main

=======

        ↓
Code từ feature/payment

>>>>>>> feature/payment

Đây là merge conflict.

7. Tự resolve

Bạn quyết định:

Cả login và payment đều cần giữ.

Sửa thành:

def login():
    print("Login by Developer A")


def payment():
    print("Payment by Developer B")


print("Hello")

Xóa toàn bộ:

<<<<<<<
=======
>>>>>>>

Sau đó:

git status

Git sẽ nói rằng có file conflict đã được giải quyết nhưng cần stage.

git add app.py

Sau đó:

git commit

Git có thể tự tạo merge commit message.

Hoặc:

git commit -m "Merge payment feature"
8. Nhìn lại lịch sử

Đây là lúc git log --graph cực kỳ thú vị:

git log --oneline --graph --all

Bạn sẽ thấy dạng:

*   Merge payment feature
|\
| * Add payment feature
* | Add login feature
|/
* Initial project

Đây chính là Git graph thực tế khi team làm việc song song.

9. Tiếp tục mô phỏng Developer C

Bây giờ tạo:

git switch main
git switch -c feature/profile

Sửa:

def profile():
    print("Profile")

Commit:

git add .
git commit -m "Add profile"
10. Cố tình commit nhầm

Giả sử bạn đang ở:

feature/profile

và vô tình sửa README.md:

# Git Team Simulation

THIS WAS A MISTAKE

Sau đó:

git add .
git commit -m "Update README"

Ôi, commit nhầm.

Đây là lúc chúng ta học:

git reset
git revert

Nhưng đừng chạy ngay.

Trước tiên:

git log --oneline --graph --all

để nhìn commit.

11. Sau đó ta sẽ học reset

Ví dụ:

A -- B -- C
         ↑
       HEAD

Bạn muốn bỏ C:

git reset --soft HEAD~1

hoặc:

git reset --mixed HEAD~1

hoặc cực mạnh:

git reset --hard HEAD~1

Ba cái này khác nhau rất quan trọng.

12. Sau đó mô phỏng Remote

Đây mới là phần giống team thật.

Ta có:

Developer A
      │
      ▼
   GitHub
      ▲
      │
Developer B

Mỗi người có local repository riêng.

Bạn có thể mô phỏng bằng hai thư mục:

D:\workspace\
│
├── developer_A\
│
└── developer_B\

Clone cùng một repository:

git clone <repo> developer_A
git clone <repo> developer_B

Sau đó:

Developer A
    │
    │ push
    ▼
  remote
    ▲
    │ pull
Developer B

Lúc này bạn sẽ gặp những lỗi rất thực tế như:

! [rejected] main -> main (non-fast-forward)

và phải xử lý:

git pull

hoặc:

git fetch
git merge

hoặc:

git pull --rebase
13. Mình khuyên bạn học theo thứ tự này

Đừng học Git bằng cách thuộc lòng command. Hãy tạo một repo duy nhất và phá nó.

Level 1 — Cơ bản
git init
git status
git add
git commit
git log
git diff
Level 2 — Branch
git branch
git switch
git switch -c
git branch -m
git branch -d
Level 3 — Merge
git merge

Cố tình tạo:

merge conflict

rồi tự resolve.

Level 4 — Undo

Học thật kỹ:

git restore
git reset
git revert

Đây là phần rất quan trọng khi làm team.

Level 5 — Remote
git clone
git remote
git fetch
git pull
git push
Level 6 — Team conflict

Cố tình tạo:

non-fast-forward
merge conflict
push rejected
Level 7 — Rebase
git rebase
git rebase -i

Sau khi hiểu merge rồi mới học rebase. Nếu học ngược rất dễ loạn.

Và mình đề xuất cách học với bạn

Chúng ta có thể thực sự chơi một bài lab Git, từng bước một.

Mình đưa cho bạn tình huống giống công ty, ví dụ:

Team:
  Thang       → Developer
  An          → Developer
  Minh        → Developer
  main        → production
  develop     → development

Task:
  #101 Login
  #102 Payment
  #103 User Profile

Mình sẽ không đưa sẵn cách giải.

Mình đưa tình huống → bạn chạy Git → cố tình gặp lỗi → paste output cho mình → mình giải thích Git đang nghĩ gì bên trong, rồi cho tình huống tiếp theo.

Cách này sẽ giúp bạn hiểu được branch, HEAD, commit, merge, conflict, remote, fetch, pull, rebase bằng thực hành chứ không phải học thuộc lệnh.
```
# cách khắc phục khi lỡ commit key bị lỗi push nhưng khi fix xong thì lại không push lên được nữa
```bash
Điểm quan trọng là: Git lưu lịch sử commit. Việc bạn sửa file rồi commit lần 2 không xóa secret khỏi commit lần 1.

Ví dụ:
    Commit A: code + API_KEY=abc123    ← secret vẫn nằm ở đây
           ↓
    Commit B: xóa API_KEY              ← hiện tại đã sạch
           ↓
    git push
-> GitHub vẫn thấy abc123 trong Commit A, nên GitHub Secret Scanning/Push Protection có thể chặn push.
```
**Nếu commit chứa secret chưa từng push lên GitHub**
```bash
Đây là trường hợp dễ xử lý nhất.
Ví dụ lịch sử của bạn:
A -- B -- C

Trong đó C là commit chứa key.
Nếu muốn xóa commit C và tạo lại commit sạch, có thể:
git reset --soft HEAD~1

Sau đó:
git status

File vẫn còn các thay đổi nhưng commit cuối đã bị bỏ.
Bạn sửa secret:
nano config.py

Sau đó:
git add .
git commit -m "initial commit"
git push

Lúc này lịch sử local sẽ không còn commit chứa secret.
```
Nếu secret nằm sâu nhiều commit
Ví dụ:
A
↓
B
↓
C  ← chứa API key
↓
D
↓
E  ← hiện tại

Bạn không thể chỉ sửa file rồi:
git add .
git commit

vì:
A
↓
B
↓
C  ← secret vẫn tồn tại
↓
D
↓
E  ← đã sửa
↓
F  ← commit mới

Secret vẫn nằm trong C.
Lúc này thường dùng:
git rebase -i

để sửa/xóa commit cũ.
Ví dụ:
git rebase -i HEAD~5

Git sẽ mở danh sách:
pick abc111 commit A
pick abc222 commit B
pick abc333 commit C
pick abc444 commit D
pick abc555 commit E

Bạn có thể đổi commit cần sửa từ:
pick abc333 commit C

thành:
edit abc333 commit C

Sau đó Git dừng tại commit đó để bạn sửa lại.
3. Nếu secret đã từng push lên GitHub
Đây là trường hợp khác hẳn.
Ví dụ:
Local:

A → B → C(secret) → D

và bạn đã:
git push

thì secret đã tồn tại trên GitHub.
Ngay cả khi bạn làm:
git commit -m "remove secret"
git push

thì GitHub vẫn có:
C(secret)
↓
D
↓
E(remove secret)

Do đó phải xử lý hai việc:
Việc 1: Thu hồi/thay đổi secret
Ví dụ API key:
OLD_KEY = abc123

thì phải tạo key mới và vô hiệu hóa key cũ.
Đây là việc rất quan trọng.
Không nên chỉ xóa key khỏi Git history rồi tiếp tục sử dụng key cũ.
Việc 2: Xóa secret khỏi Git history
Với repository lớn hoặc lịch sử phức tạp, công cụ hiện đại thường dùng là:
git filter-repo

Ví dụ nếu muốn xóa toàn bộ file:
git filter-repo --path .env --invert-paths

Hoặc nếu cần thay thế một secret cụ thể trong toàn bộ history thì có thể dùng --replace-text.
Sau đó thường phải force push:
git push --force

Nhưng force push có thể ảnh hưởng người khác đang làm việc trên repository, nên cần cẩn thận.
4. Một trường hợp rất hay gặp với GitHub
Giả sử bạn làm:
echo "API_KEY=abc123" > .env

git add .
git commit -m "add project"
git push

GitHub báo:
Push cannot contain secrets

Bạn nghĩ:
# sửa .env
API_KEY=

rồi:
git add .
git commit -m "remove api key"
git push

Nhưng vẫn bị chặn.
Lý do là Git đang push:
commit 1
└── .env chứa abc123  ← GitHub phát hiện

commit 2
└── .env đã sửa

GitHub không chỉ kiểm tra file hiện tại, mà có thể kiểm tra các commit đang được push.
5. Cách phòng tránh tốt nhất
Với project bình thường, mình khuyên cấu trúc như này:
project/
├── .git/
├── src/
├── README.md
├── .gitignore
├── .env.example
└── .env

.gitignore:
.env
.env.*
!.env.example

.env:
API_KEY=abc123
DATABASE_PASSWORD=123456

Không commit .env.
Còn .env.example:
API_KEY=
DATABASE_PASSWORD=

thì commit:
git add .gitignore .env.example
git commit -m "add environment config example"

Người khác clone project về thì:
cp .env.example .env

rồi tự điền key.
6. Quan trọng nhất: phân biệt 3 tình huống
Bạn có thể nhớ bảng này:
Tình huống	Cách xử lý
Secret nằm trong file nhưng chưa commit	Sửa file → git add → commit
Secret nằm trong commit cuối, chưa push	git reset --soft HEAD~1 → sửa → commit lại
Secret nằm trong commit cũ, chưa push	git rebase -i để sửa lịch sử
Secret đã push lên GitHub	Thu hồi/thay key + rewrite Git history
Secret đã push và repository có nhiều người dùng	Rewrite history + phối hợp với team


Một nguyên tắc cực kỳ quan trọng:
Secret đã từng xuất hiện trong Git thì hãy coi secret đó đã bị lộ, kể cả bạn đã xóa nó trong commit sau.

Nếu bạn đang gặp đúng tình huống hiện tại là GitHub đang chặn git push vì phát hiện secret, bạn có thể gửi cho tôi nguyên văn output của git push. Tôi có thể chỉ cho bạn từng lệnh để xử lý mà không làm mất code hiện tại.