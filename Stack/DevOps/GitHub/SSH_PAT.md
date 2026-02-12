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
PAT (Personal Acess Token)
Dùng khi git/gitHub yêu cầu tài khoản và mật khẩu: nếu remote là http thì mật khẩu phải nhập là PAT
    1. 1. https://github.com/settings/tokens
    2. 2. Chọn generate new tokenTokens → (classic)
    3. 3. Note: push with git
    4. 4. Expiration: 90 days hoặc No expiration
    5. 5. Scopes: tick repo (để push code)
    6. 6. Nhấn Generate token
    7. 7. Copy chuỗi token đó - chỉ hiện 1 lần
    8. Khi git push, nhập: Username: thang170725, Password: dán token vừa tạo
    9. Lưu token để không phải nhập lại: git config --global credential.helper store