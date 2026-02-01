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