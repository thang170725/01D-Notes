# Cách dùng SSH key để push/pull
```bash
1. Kiểm tra xem đã có SSH key chưa: ls ~/.ssh
2. Tạo key nếu chưa có: ssh-keygen -t ed25519 -C "your_email@example.com" -> rồi nhấn enter liên tục
3. Copy nội dung public key: cat ~/.ssh/id_ed25519.pub
4. Thêm vào gitHub
    1. https://github.com/settings/keys
    2. New SSH key
    3. Title: đặt tên cho key ví dụ ubuntu laptop
    4. Dán key 
    5. Add SSH key
5. Đổi remote từ HTTPS sang SSH: git remote set-url origin git@github.com:thang170725/elgamal.git
```