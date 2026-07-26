- [git checkout (Tạo nhánh và chuyển sang nhánh đó (đây là cách cũ))](#git-checkout-tạo-nhánh-và-chuyển-sang-nhánh-đó-đây-là-cách-cũ)
  - [-b](#-b)
  - [--orphan (Tạo branch mới không có lịch sử)](#--orphan-tạo-branch-mới-không-có-lịch-sử)
- [git branch (Dùng để tạo nhánh mới nhưng chưa chuyển sang)](#git-branch-dùng-để-tạo-nhánh-mới-nhưng-chưa-chuyển-sang)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
    - [-l \& --list (chỉ liệt kê local branches trên máy của bạn, không phải toàn bộ nhánh trên GitHub)](#-l----list-chỉ-liệt-kê-local-branches-trên-máy-của-bạn-không-phải-toàn-bộ-nhánh-trên-github)
    - [-a (Để xem nhánh trên cả local + remote.)](#-a-để-xem-nhánh-trên-cả-local--remote)
    - [-r (liệt kê remote-tracking branches)](#-r-liệt-kê-remote-tracking-branches)
  - [Update (Nhóm cập cật)](#update-nhóm-cập-cật)
    - [-m](#-m)
  - [Remove (Nhóm xóa)](#remove-nhóm-xóa)
    - [-D (xóa branch)](#-d-xóa-branch)
    - [-d (xóa nhanh trên máy local)](#-d-xóa-nhanh-trên-máy-local)
- [git switch (vừa tạo branch vừa checkout sáng branch đó đây là cách mới)](#git-switch-vừa-tạo-branch-vừa-checkout-sáng-branch-đó-đây-là-cách-mới)
  - [-c](#-c)
- [git fetch](#git-fetch)
  - [--prune](#--prune)
- [git merge (gộp lịch sử commit, tức áp dụng các thay đổi (changes/diffs), không phải cộng file kiểu union)](#git-merge-gộp-lịch-sử-commit-tức-áp-dụng-các-thay-đổi-changesdiffs-không-phải-cộng-file-kiểu-union)
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
### -m
**Ex**
```bash
git branch -m main # đổi tên thành main
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
## -c
```bash
git switch -c dev2 # -c = create
```
# git fetch
```bash
- Nó làm gì?
    + Git đi hỏi GitHub:
        - Có commit mới nào không?
        - Có branch mới nào không?
        - Có branch nào thay đổi không?
    + rồi cập nhật các remote-tracking branch:
        - origin/main
        - origin/dev2
    + Nó KHÔNG:
        - không sửa code working directory của bạn
        - không merge vào branch đang đứng
        - không commit gì cả
    => An toàn.
- Ví dụ: git fetch origin = lấy thông tin / commit mới từ remote (origin) về, nhưng không merge vào branch hiện tại.
```
## --prune
```bash
git fetch --prune # --prune dọn các remote-tracking branch đã bị xóa
```
commgit push –set-upstream origin nhanh_1
Push lên central repo bằng nhanh_1 khoong phải là nhánh chính


Tái cơ sở cho một nhánh
Git rebase –continue
Git rebase –skip

Git reset –soft <commit id>
Di chuyển head về vị triis commit trạng thái của stage và tất cả sử thay đổi của file được giữ nguyên
Git reset <commit id>
Di chuyển head về vị trí commiit reset vẫn giữ tất cả thay đổi của file, nhưng loại bỏ các thay đổi stage
Git reset –hard <commit id>
Di chuyển con trỏ head về vị trí commit reset và loại bỏ tất cả sử thay đổi của file
Git revert <commit id>
Quay lại commit trước đây
bỏ qua file không cần giám sát





Diff file1 file2 : tìm kiếm sự khác biệt giữa file1 và file2
Repository : kho lưu trữ
Commit : một đơn vị làm việc
Branch : nhánh
Main/ master : tên của repo chính
Merge/ rebase : kết hợp 2 nhánh
Develop : tên của nhánh, lập trình viên






git fetch
Lấy các thông tin về commit mới từ central, kiểm tra sự thay đổi.
Cú pháp:
    1. git fetch origin (Lệnh này giúp Git cập nhật tất cả thông tin mới từ GitHub bao gồm nhánh mới của bạn bè)
git status
Hiển thị trạng thái của kho lưu trữ.
# git merge (gộp lịch sử commit, tức áp dụng các thay đổi (changes/diffs), không phải cộng file kiểu union)
```bash
"Fast-forward" nghĩa là gì?
  Lịch sử kiểu này:
    A---B---C   (dev1)         \          D---E (feature/login)
  
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