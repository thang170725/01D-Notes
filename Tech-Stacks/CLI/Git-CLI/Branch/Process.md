- [git checkout (Tạo nhánh và chuyển sang nhánh đó (đây là cách cũ))](#git-checkout-tạo-nhánh-và-chuyển-sang-nhánh-đó-đây-là-cách-cũ)
  - [-b](#-b)
  - [--orphan (Tạo branch mới không có lịch sử)](#--orphan-tạo-branch-mới-không-có-lịch-sử)
- [git branch (Dùng để tạo nhánh mới nhưng chưa chuyển sang)](#git-branch-dùng-để-tạo-nhánh-mới-nhưng-chưa-chuyển-sang)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
    - [-l \& --list (chỉ liệt kê local branches trên máy của bạn, không phải toàn bộ nhánh trên GitHub)](#-l----list-chỉ-liệt-kê-local-branches-trên-máy-của-bạn-không-phải-toàn-bộ-nhánh-trên-github)
    - [-a (Để xem nhánh trên cả local + remote.)](#-a-để-xem-nhánh-trên-cả-local--remote)
    - [-r (liệt kê remote-tracking branches)](#-r-liệt-kê-remote-tracking-branches)
  - [Update (Nhóm cập cật)](#update-nhóm-cập-cật)
    - [-m (đổi tên nhánh)](#-m-đổi-tên-nhánh)
    - [-M (đổi tên nhánh và force)](#-m-đổi-tên-nhánh-và-force)
  - [Remove (Nhóm xóa)](#remove-nhóm-xóa)
    - [-D (xóa branch)](#-d-xóa-branch)
    - [-d (xóa nhanh trên máy local)](#-d-xóa-nhanh-trên-máy-local)
- [git switch (vừa tạo branch vừa checkout sáng branch đó đây là cách mới)](#git-switch-vừa-tạo-branch-vừa-checkout-sáng-branch-đó-đây-là-cách-mới)
  - [-c (tạo nhánh mới đồng thời chuyển qua nhánh mới)](#-c-tạo-nhánh-mới-đồng-thời-chuyển-qua-nhánh-mới)
- [git fetch (Lấy các thông tin về commit mới từ central, kiểm tra sự thay đổi)](#git-fetch-lấy-các-thông-tin-về-commit-mới-từ-central-kiểm-tra-sự-thay-đổi)
  - [--prune](#--prune)
- [git rebase (Tái cơ sở cho một nhánh)](#git-rebase-tái-cơ-sở-cho-một-nhánh)
- [print("Hello from main")](#printhello-from-main)
- [sửa file conflict](#sửa-file-conflict)
- [test code](#test-code)
- [1. đang ở feature branch](#1-đang-ở-feature-branch)
- [2. lấy main mới nhất](#2-lấy-main-mới-nhất)
- [3. đưa feature lên nền main mới nhất](#3-đưa-feature-lên-nền-main-mới-nhất)
- [4. nếu conflict:](#4-nếu-conflict)
- [sửa file](#sửa-file)
- [5. nếu muốn hủy](#5-nếu-muốn-hủy)
- [6. sau khi thành công](#6-sau-khi-thành-công)
  - [–continue](#continue)
  - [–skip](#skip)
- [git merge (gộp lịch sử commit, tức áp dụng các thay đổi (changes/diffs), không phải cộng file kiểu union)](#git-merge-gộp-lịch-sử-commit-tức-áp-dụng-các-thay-đổi-changesdiffs-không-phải-cộng-file-kiểu-union)
- [`cherry-pick`, `interactive rebase`  dùng như thế nào](#cherry-pick-interactive-rebase--dùng-như-thế-nào)
---
# git checkout (Tạo nhánh và chuyển sang nhánh đó (đây là cách cũ))
## -b
**Ex**
```bash
git checkout -b feature/login origin/feature/login # Tạo branch tên feature/login rồi chuyển sang đó

# nghĩa là: 
# git branch feature/login
# git checkout feature/login
```
## --orphan (Tạo branch mới không có lịch sử)
**Ex**
```bash
git checkout --orphan new-main # tạo branch new-main không có lịch sử
```
# git branch (Dùng để tạo nhánh mới nhưng chưa chuyển sang)
**Ex**
```bash
git branch dev2 # tạo nhánh dev2 nhưng chưa chuyển sang
```
## Display (Nhóm cung cấp thông tin)
### -l & --list (chỉ liệt kê local branches trên máy của bạn, không phải toàn bộ nhánh trên GitHub)
**Syn**
```bash
1. git branch
2. git branch -l
3. git branch --list
```
### -a (Để xem nhánh trên cả local + remote.)
**Syn**
```bash
git branch -a
```
### -r (liệt kê remote-tracking branches)
```bash
“remote-tracking branch” là gì?
  - Không phải branch thật trên GitHub, cũng không phải branch local bạn code.
  - Nó là bản ghi local của bạn về branch trên remote.
```
**Ex**
```bash
git branch -r 
# origin/HEAD -> origin/main
# origin/feature/login
# origin/main

# nghĩa là Git của bạn biết remote origin có:
# branch main
# branch feature/login
```
## Update (Nhóm cập cật)
### -m (đổi tên nhánh)
**Ex**
```bash
git branch -m main # đổi tên thành main
```
### -M (đổi tên nhánh và force)
```bash
tức là -M = -m + force
```
## Remove (Nhóm xóa)
### -D (xóa branch)
**Ex**
```bash
git branch -D main
```
### -d (xóa nhanh trên máy local)
**Syn**
```bash
git branch -d <branch_name>
```
# git switch (vừa tạo branch vừa checkout sáng branch đó đây là cách mới)
## -c (tạo nhánh mới đồng thời chuyển qua nhánh mới)
```bash
git switch -c dev2 # -c = create
```
# git fetch (Lấy các thông tin về commit mới từ central, kiểm tra sự thay đổi)
**Nó làm gì?**
```bash
Git đi hỏi GitHub:
  - Có commit mới nào không?
  - Có branch mới nào không?
  - Có branch nào thay đổi không?

rồi cập nhật các remote-tracking branch:
  - origin/main
  - origin/dev2

Nó KHÔNG:
  - không sửa code working directory của bạn
  - không merge vào branch đang đứng
  - không commit gì cả
=> An toàn.
```
**Syn**
```bash
git fetch origin # lấy thông tin / commit mới từ remote (origin) về, nhưng không merge vào branch hiện tại.
```
## --prune
```bash
git fetch --prune # --prune dọn các remote-tracking branch đã bị xóa
```
# git rebase (Tái cơ sở cho một nhánh)
git rebase là một trong những phần quan trọng nhất của Git. Nếu hiểu đúng bản chất, bạn sẽ thấy nó khá đơn giản.

1. Rebase dùng để làm gì?

Giả sử bạn có:

A---B---C   main
     \
      D---E   feature

Bạn đang làm ở branch feature, trong khi main đã có thêm commit C.

Bạn muốn đưa các thay đổi của main vào feature.

Có 2 cách phổ biến:

Cách 1: merge
git checkout feature
git merge main

Kết quả:

A---B---C------M   feature
     \        /
      D------E

Có thêm một merge commit M.

Cách 2: rebase
git checkout feature
git rebase main

Git sẽ "bê" các commit D, E lên trên C:

A---B---C---D'---E'   feature

Lưu ý: D', E' không phải commit cũ, mà là các commit mới có nội dung tương đương.

2. Mental model dễ nhớ

Hãy nghĩ:

merge = nối hai lịch sử lại với nhau

rebase = đặt lại nền của branch

Ví dụ ban đầu:

main:     A---B---C
               \
feature:        D---E

Bạn nói:

"Feature của tôi được xây dựng từ B, nhưng giờ main đã lên C. Tôi muốn feature của tôi như thể nó được phát triển từ C ngay từ đầu."

Thì:

git rebase main

Kết quả:

main:     A---B---C
                  \
feature:           D'---E'
3. Quy trình rebase thường dùng

Ví dụ bạn đang code trên:

feature/login

và muốn cập nhật nó theo main.

Bước 1: kiểm tra branch
git branch

Ví dụ:

* feature/login
  main

Dấu * cho biết bạn đang ở feature/login.

Bước 2: lấy thông tin mới nhất từ remote
git fetch origin

Lệnh này cập nhật thông tin về remote nhưng không tự merge code vào branch của bạn.

Bước 3: rebase lên main mới nhất
git rebase origin/main

Git sẽ lấy các commit của bạn rồi đặt chúng lên origin/main.

Ví dụ:

Trước:

origin/main: A---B---C

feature:          \---D---E

Sau:

origin/main: A---B---C
                    \
feature:             D'---E'
4. Nếu xảy ra conflict thì sao?

Đây là phần quan trọng nhất.

Ví dụ:

git rebase origin/main

Git báo:

CONFLICT (content): Merge conflict in app.py

Git dừng lại.

Bạn mở app.py:

<<<<<<< HEAD
print("Hello from main")
=======
print("Hello from feature")
>>>>>>> abc123

Bạn tự quyết định code đúng là gì.

Ví dụ sửa thành:

print("Hello from feature")

Sau đó:

git add app.py

Rồi:

git rebase --continue
5. Nếu còn conflict

Git có thể tiếp tục báo conflict.

Bạn cứ lặp:

fix conflict
    ↓
git add <file>
    ↓
git rebase --continue
    ↓
fix conflict tiếp nếu có

Cho đến khi:

Successfully rebased and updated refs/heads/feature/login.
6. Nếu thấy rebase quá rối thì hủy

Bạn có thể quay lại trạng thái trước khi rebase:

git rebase --abort

Ví dụ:

feature trước rebase
        ↓
git rebase origin/main
        ↓
CONFLICT
        ↓
không muốn xử lý nữa
        ↓
git rebase --abort
        ↓
quay lại trạng thái trước rebase

Đây là một lệnh rất đáng nhớ.

7. Một ví dụ thực tế đầy đủ

Giả sử bạn có:

main
 ├── A
 ├── B
 └── C

feature
 ├── D
 └── E

Bạn đang ở feature.

Trước tiên:

git status

Nếu có code chưa commit thì nên xử lý trước.

Sau đó:

git fetch origin
git rebase origin/main

Nếu không conflict:

Done

Nếu conflict:

# sửa file conflict

git add .
git rebase --continue

Nếu tiếp tục conflict thì lại sửa → git add → git rebase --continue.

Nếu muốn bỏ:

git rebase --abort
8. Một điểm rất quan trọng: rebase làm thay đổi commit history

Đây là lý do phải cẩn thận.

Ví dụ trước:

A---B---D---E

Sau rebase:

A---B---C---D'---E'

D' và E' có commit hash mới.

Vì vậy:

Không nên tùy tiện rebase một branch mà nhiều người khác đang cùng làm.

Ví dụ branch:

feature/thang-login

chỉ mình bạn làm → rebase thường khá an toàn.

Nhưng branch:

main
develop
team-shared-feature

nhiều người cùng dựa vào → cần cực kỳ cẩn thận.

9. Rebase rồi push thì sao?

Đây là chỗ người mới hay gặp lỗi.

Bạn đã push:

remote feature:

A---B---D---E

Sau đó local rebase:

A---B---C---D'---E'

Nếu chạy:

git push

có thể Git từ chối:

rejected
non-fast-forward

Vì lịch sử remote và local đã khác nhau.

Trong trường hợp branch chỉ mình bạn sử dụng, thường dùng:

git push --force-with-lease

Nên ưu tiên:

git push --force-with-lease

thay vì:

git push --force

--force-with-lease an toàn hơn vì Git sẽ kiểm tra xem remote có bị người khác cập nhật ngoài dự kiến hay không.

10. git rebase -i là gì?

Ngoài việc cập nhật branch, rebase còn có một tính năng cực kỳ hay:

git rebase -i HEAD~3

-i = interactive.

Ví dụ bạn có:

A---B---C---D

Bạn muốn chỉnh 3 commit gần nhất:

git rebase -i HEAD~3

Git mở:

pick abc123 Add login
pick def456 Fix login
pick ghi789 Fix login again

Bạn có thể đổi:

pick abc123 Add login
squash def456 Fix login
squash ghi789 Fix login again

Kết quả:

A---B---C'

Ba commit được gộp thành một commit.

11. Các keyword quan trọng của interactive rebase
pick    = giữ commit
reword  = đổi commit message
edit    = dừng lại để chỉnh commit
squash  = gộp commit vào commit trước
fixup   = gộp commit, bỏ message của nó
drop    = xóa commit

Ví dụ bạn có:

A
B Add login
C Fix typo
D Fix another typo
E Add test

Bạn có thể biến thành:

A
B Add login
C Add test

bằng cách squash/drop các commit không cần thiết.

12. Merge vs Rebase
	merge	rebase
Giữ nguyên history	✅	❌
Tạo merge commit	Có thể	❌
History sạch	⭐⭐⭐	⭐⭐⭐⭐⭐
Thay đổi commit hash	❌	✅
An toàn với shared branch	✅	Cẩn thận
Thường dùng trên feature branch	✅	✅
13. Workflow mà bạn sẽ gặp rất nhiều

Giả sử team có:

main

Bạn tạo:

feature/login

Trong lúc bạn code, người khác merge code vào main.

Bạn muốn cập nhật feature:

git fetch origin
git rebase origin/main

Sau đó:

# test code

git push --force-with-lease

Cuối cùng tạo PR:

main
  │
  ├── A
  ├── B
  ├── C
  │
  └── feature/login
          D'
          E'

History rất sạch.

14. Một workflow thực tế nên nhớ

Nếu bạn đang làm feature branch cá nhân:

# 1. đang ở feature branch
git status

# 2. lấy main mới nhất
git fetch origin

# 3. đưa feature lên nền main mới nhất
git rebase origin/main

# 4. nếu conflict:
# sửa file
git add .
git rebase --continue

# 5. nếu muốn hủy
git rebase --abort

# 6. sau khi thành công
git push --force-with-lease
Chỉ cần nhớ 4 câu này:
git fetch
    ↓
git rebase origin/main
    ↓
fix conflict → git add → git rebase --continue
    ↓
git push --force-with-lease

Điểm quan trọng nhất: rebase không phải là "merge nhưng khác cú pháp". Nó viết lại lịch sử commit bằng cách tạo lại các commit của branch trên một base mới. Vì vậy nó rất hữu ích để giữ history sạch, nhưng phải cẩn thận với branch đã được người khác sử dụng.
## –continue
## –skip
# git merge (gộp lịch sử commit, tức áp dụng các thay đổi (changes/diffs), không phải cộng file kiểu union)
```bash
"Fast-forward" nghĩa là gì?
  Lịch sử kiểu này:
    A---B---C   (dev1)
             \          D---E (feature/login)
  
  Nếu dev1 vẫn ở C và feature/login chỉ đi tiếp từ đó:
    Git chỉ kéo con trỏ:
      A---B---C---D---E
    dev1 trỏ sang E.
  => Đó là fast-forward.
```
**Ex**
```bash
# tại nhánh main chạy lệnh
thang@PhatToNhuLai:~/workspace/test/github-test/dev1$ git merge feature/login # gom nhánh feature/login vào main
# Updating 2c13965..cc60419
# Fast-forward
#  login.txt | 2 ++
#  test.txt  | 3 ---
#  2 files changed, 2 insertions(+), 3 deletions(-)
#  create mode 100644 login.txt
#  delete mode 100644 test.txt

Merge đã mang những thay đổi đó sang branch hiện tại.
Nên kết quả:
login.txt   ✅
test.txt    bị xóa
=> hoàn toàn đúng.

Vì sao không còn cả hai file?
Giả sử: 
- Branch A (dev1)
    + test.txt
- Branch B (feature/login), ai đó làm:
    1. rm test.txt
    2. touch login.txt
    3. git commit
    => thì B bây giờ là: login.txt
Merge B vào A 
    - không phải: test.txt + login.txt
    - mà là: áp dụng thay đổi từ B:
        1. xóa test.txt
        2. thêm login.txt
```
# `cherry-pick`, `interactive rebase`  dùng như thế nào
Hai cái này rất hay đi cùng nhau, nhưng mục đích hoàn toàn khác nhau:

git cherry-pick → lấy một/vài commit cụ thể từ branch khác sang branch hiện tại
git rebase -i → chỉnh sửa lịch sử commit của chính branch hiện tại: gộp, đổi message, đổi thứ tự, xóa commit...

Hãy nhìn ví dụ này:

A---B---C---D---E   main
     \
      F---G---H     feature
1. git cherry-pick là gì?

Giả sử bạn đang ở main:

A---B---C---D---E   main
     \
      F---G---H     feature

Trong feature, commit G có một bug fix rất quan trọng.

Bạn không muốn lấy F và H, chỉ muốn lấy đúng G.

Đây chính là lúc dùng:

git cherry-pick <commit-hash>

Ví dụ:

git cherry-pick abc123

Kết quả:

A---B---C---D---E---G'   main
     \
      F---G---H           feature

Git tạo một commit mới G' trên main.

Mental model

cherry-pick = "Tôi chỉ muốn lấy commit này, không cần cả branch."

2. Tìm commit hash

Dùng:

git log --oneline

Ví dụ:

a8f1234 Fix authentication bug
c9d4567 Add logging
e1a7890 Add login API
b2c3456 Initial commit

Bạn muốn lấy:

a8f1234 Fix authentication bug

thì:

git cherry-pick a8f1234
3. Ví dụ thực tế

Giả sử:

main:

A---B---C

Bạn có branch:

feature/payment:

A---B---C---D---E---F

Trong đó:

D = thêm payment API
E = sửa typo
F = fix security bug

Bạn phát hiện F rất quan trọng và muốn đưa riêng nó vào main.

Đầu tiên:

git checkout main

Sau đó:

git cherry-pick F

Kết quả:

A---B---C---F'       main
         \
          D---E---F  feature/payment

main nhận được thay đổi của F nhưng không nhận D và E.

4. Cherry-pick nhiều commit

Có thể lấy nhiều commit:

git cherry-pick abc123 def456 ghi789

Ví dụ:

git cherry-pick D F

Kết quả:

A---B---C---D'---F'   main
         \
          D---E---F   feature
5. Cherry-pick một khoảng commit

Ví dụ:

A---B---C---D---E---F---G

Muốn lấy D, E, F:

git cherry-pick C..F

Điểm hơi dễ nhầm:

C..F

nghĩa là:

Các commit sau C cho đến F.

Tức:

D E F
6. Nếu cherry-pick bị conflict

Ví dụ:

git cherry-pick abc123

Git báo:

CONFLICT (content): Merge conflict in app.py

Bạn sửa conflict.

Sau đó:

git add app.py
git cherry-pick --continue

Nếu muốn bỏ toàn bộ cherry-pick:

git cherry-pick --abort

Mental model:

cherry-pick
    ↓
conflict
    ↓
sửa file
    ↓
git add
    ↓
git cherry-pick --continue
7. Vậy interactive rebase là gì?

Bây giờ giả sử branch của bạn:

A---B---C---D---E---F

Bạn nhìn history và thấy:

C = Add login
D = Fix typo
E = Fix typo again
F = Add tests

Bạn muốn history đẹp hơn:

A---B---C'---F'

Trong đó D, E được gộp vào C.

Dùng:

git rebase -i HEAD~4

-i = interactive.

8. Git sẽ cho bạn một danh sách

Ví dụ:

pick abc123 Add login
pick def456 Fix typo
pick ghi789 Fix typo again
pick jkl012 Add tests

Bạn có thể sửa thành:

pick abc123 Add login
squash def456 Fix typo
squash ghi789 Fix typo again
pick jkl012 Add tests

Sau đó Git sẽ gộp:

Add login
 + Fix typo
 + Fix typo again

thành một commit.

Kết quả:

A---B---C'---F'
9. squash nghĩa là gì?

Đây là keyword cực kỳ quan trọng.

pick   = giữ commit
squash = gộp commit vào commit phía trước
fixup  = gộp vào commit phía trước, bỏ commit message
reword = đổi commit message
edit   = dừng lại để bạn chỉnh commit
drop   = xóa commit

Ví dụ ban đầu:

A
B Add login
C fix typo
D fix typo again
E fix login bug
F add test

Bạn có thể biến thành:

A
B Add login
C fix login bug
D add test

bằng interactive rebase.

10. reword — đổi commit message

Giả sử:

A---B---C

Commit:

C = update

Message quá tệ 😅.

Bạn chạy:

git rebase -i HEAD~1

Thấy:

pick abc123 update

đổi thành:

reword abc123 update

Git sẽ cho bạn sửa message:

Add user authentication
11. drop — xóa commit

Ví dụ:

A---B---C---D---E

Bạn phát hiện D là commit không cần thiết.

git rebase -i HEAD~3

Có thể thấy:

pick C
pick D
pick E

đổi thành:

pick C
drop D
pick E

Kết quả:

A---B---C---E'
12. fixup khác squash như thế nào?

Ví dụ:

pick A Add login
fixup B Fix typo
fixup C Fix another typo

Git sẽ tạo:

Add login

và bỏ qua commit message của B, C.

Trong khi:

squash

thường sẽ cho bạn cơ hội chỉnh/gộp commit messages.

Thực tế

Nếu bạn có:

A Add login
B fix typo
C fix typo again

Thường muốn:

A Add login

thì dùng:

pick A
fixup B
fixup C

rất tiện.

13. Đổi thứ tự commit

Đây cũng là một điểm rất mạnh.

Ban đầu:

A---B---C---D

Interactive rebase:

git rebase -i HEAD~3

Git đưa:

pick B
pick C
pick D

Bạn có thể đổi:

pick D
pick B
pick C

Git sẽ cố xây dựng lại history theo thứ tự mới.

Nhưng: đổi thứ tự có thể tạo conflict nếu các commit phụ thuộc lẫn nhau.

14. cherry-pick vs rebase -i

Đây là phần quan trọng nhất:

	Cherry-pick	Interactive rebase
Mục đích	Lấy commit từ nơi khác	Chỉnh history
Lấy commit cụ thể	✅	Không phải mục đích chính
Gộp commit	❌	✅
Đổi message	Không trực tiếp	✅
Xóa commit	Không	✅
Đổi thứ tự	Không	✅
Tạo commit mới	✅	Thường tạo lại commit
Có thể conflict	✅	✅
15. Hai tình huống thực tế
Tình huống A — dùng cherry-pick

Team có:

main
 |
 A---B---C

feature-A
 |
 A---B---C---D---E

E là một bug fix quan trọng.

Bạn muốn đưa chỉ E vào main.

git checkout main
git cherry-pick E

→ Cherry-pick.

Tình huống B — dùng interactive rebase

Bạn đang có:

feature/login

A---B---C---D---E---F

Trong đó:

C Add login
D fix typo
E fix typo again
F add tests

Trước khi tạo PR, bạn muốn history sạch:

A---B---C'---F'

D và E gộp vào C.

git rebase -i HEAD~4

→ Interactive rebase.

16. Một workflow rất phổ biến

Bạn code một feature.

Trong quá trình code:

A Add login
B fix typo
C fix typo
D debug
E remove debug
F add test

Không sao cả.

Trước khi tạo PR:

git rebase -i HEAD~5

Bạn biến thành:

A Add login
B Add tests

History nhìn rất sạch.

Sau đó:

git push --force-with-lease

Lưu ý: vì rebase đã rewrite history nên nếu branch đã push lên remote, thường cần --force-with-lease. Chỉ làm vậy khi bạn hiểu branch đó có đang được người khác dùng chung hay không.

17. Cách nhớ cực ngắn

Hãy nhớ hai câu:

cherry-pick

"Cho tôi commit này."

git cherry-pick <commit>
branch A
   │
   └── commit X
          ↓
       cherry-pick
          ↓
branch B
   └── X'
rebase -i

"Cho tôi chỉnh lại lịch sử commit của branch này."

git rebase -i HEAD~N

Rồi bạn có thể:

pick
reword
edit
squash
fixup
drop
Một mental model rất đáng nhớ
                 Git history
                      │
          ┌───────────┴───────────┐
          │                       │
     Lấy commit                 Chỉnh history
     từ nơi khác                     │
          │                    interactive rebase
     cherry-pick                     │
          │              ┌──────────┼──────────┐
          │              │          │          │
          │            squash     reword     drop
          │              │
          │          gộp commit
          │
          └── "lấy đúng commit X"

Nếu bạn đang học Git để làm việc team, thứ tự mình khuyên bạn nắm chắc là:

commit
  ↓
branch
  ↓
merge
  ↓
rebase
  ↓
cherry-pick
  ↓
interactive rebase
  ↓
reset / revert
  ↓
stash

Trong đó reset và revert là hai lệnh tiếp theo rất đáng học vì chúng liên quan trực tiếp đến câu hỏi: "lỡ commit sai rồi thì quay lại thế nào?"