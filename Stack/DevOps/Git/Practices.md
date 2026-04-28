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