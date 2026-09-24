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
  - [--abort](#--abort)
  - [-i](#-i)
  - [–continue](#continue)
  - [–skip](#skip)
- [pick (giữ commit)](#pick-giữ-commit)
- [reword (đổi commit message)](#reword-đổi-commit-message)
- [edit (dừng lại để chỉnh commit)](#edit-dừng-lại-để-chỉnh-commit)
- [squash (gộp commit vào commit trước)](#squash-gộp-commit-vào-commit-trước)
- [fixup (gộp commit, bỏ message của nó)](#fixup-gộp-commit-bỏ-message-của-nó)
- [drop (xóa commit)](#drop-xóa-commit)
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
**Ex**
```bash
Giả sử bạn có:
  A---B---C   main
       \
        D---E   feature

Bạn đang làm ở branch feature, trong khi main đã có thêm commit C.

Bạn muốn đưa các thay đổi của main vào feature.

Có 2 cách phổ biến:
  Cách 1: merge
    1. git checkout feature
    2. git merge main
    Kết quả:
      A---B---C------M   feature
           \        /
            D------E
    -> Có thêm một merge commit M.

  Cách 2: rebase
    1. git checkout feature
    2. git rebase main
    
    Git sẽ "bê" các commit D, E lên trên C:
      A---B---C---D'---E'   feature
      Lưu ý: D', E' không phải commit cũ, mà là các commit mới có nội dung tương đương.
```
**Quy trình rebase thường dùng**
```bash
Ví dụ bạn đang code trên: feature/login và muốn cập nhật nó theo main.

Bước 1: kiểm tra branch
  git branch
  # * feature/login - Dấu * cho biết bạn đang ở feature/login.
  #   main

Bước 2: lấy thông tin mới nhất từ remote
  git fetch origin # Lệnh này cập nhật thông tin về remote nhưng không tự merge code vào branch của bạn.

Bước 3: rebase lên main mới nhất
  git rebase origin/main # Đang đứng trên feature/login, lấy origin/main làm nền mới, rồi đặt các commit của feature/login lên trên nền đó.

  Ví dụ
    Ban đầu:
      main:          A──B──C
                          \
      feature/login:       D──E

      Trong đó:
      - A B C: code trên main
      - D E: code bạn đang làm trên feature/login
      
    Sau khi người khác cập nhật main:
      main:          A──B──C──F──G
                          \
      feature/login:       D──E

    Bạn đang đứng ở: git branch
      * feature/login
        main

    Sau:
      git fetch origin
      git rebase origin/main

    Git sẽ làm thành:
      main:          A──B──C──F──G
                               \
      feature/login:            D'──E'

    Tức là:
      feature/login = code mới nhất của main + code của bạn.
      Còn nếu muốn gộp feature/login vào main thì phải làm ngược lại
        Ví dụ:
          git switch main
          git merge feature/login

          Khi đó mới là:
            main:          A──B──C──F──G──D──E

          Tức là đưa code của feature/login vào main.
          
          Vì vậy 2 câu lệnh này hoàn toàn khác nhau
          
          Đang ở feature:
            git rebase origin/main → main làm nền cho feature.
              
              main ────────────────┐
                                   ↓
              feature ───────────── code của feature

          Đang ở main: git merge feature/login → đưa feature vào main.
            feature ─────────────┐
                                 ↓
            main ─────────────── code của feature

          Và có một chi tiết quan trọng: origin/main là main trên remote, không nhất thiết là branch main local của bạn.

          Vì vậy chuỗi:
            git switch feature/login
            git fetch origin
            git rebase origin/main

          rất hợp lý khi mục đích là:
            "Tôi đang làm feature, hãy cập nhật feature của tôi dựa trên main mới nhất, nhưng đừng đưa feature của tôi vào main."

          Nếu bạn muốn, mình có thể giải thích tiếp `merge` vs `rebase` bằng một sơ đồ commit rất trực quan, vì đây là chỗ người mới dùng Git rất dễ nhầm.
```
**Nếu xảy ra conflict thì sao?**
```bash
Nếu: git rebase origin/main
  Git báo: CONFLICT (content): Merge conflict in app.py -> Git dừng lại.

Bạn mở app.py:
<<<<<<< HEAD
print("Hello from main")
=======
print("Hello from feature")
>>>>>>> abc123
-> Bạn tự quyết định code đúng là gì.

Sau đó: git add app.py

Rồi: git rebase --continue
```
## --abort
**Ex**
```bash
feature trước rebase -> git rebase origin/main -> CONFLICT -> không muốn xử lý nữa -> git rebase --abort -> quay lại trạng thái trước rebase
```
## -i
**Ex**
```bash
git rebase -i HEAD~3 # -i = interactive.
```
**Ex2**
```bash
A---B---C---D -> Bạn muốn chỉnh 3 commit gần nhất:

git rebase -i HEAD~3

Git mở:
  pick abc123 Add login
  pick def456 Fix login
  pick ghi789 Fix login again

Bạn có thể đổi:
  pick abc123 Add login
  squash def456 Fix login
  squash ghi789 Fix login again

Kết quả: A---B---C'
```
## –continue
## –skip
# pick (giữ commit)
# reword (đổi commit message)
# edit (dừng lại để chỉnh commit)
# squash (gộp commit vào commit trước)
# fixup (gộp commit, bỏ message của nó)
# drop (xóa commit)
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