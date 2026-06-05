- [GitHub Actions (tự động hóa quy trình phát triển phần mềm (CI/CD – Continuous Integration / Continuous Delivery).)](#github-actions-tự-động-hóa-quy-trình-phát-triển-phần-mềm-cicd--continuous-integration--continuous-delivery)
- [Practices](#practices)
  - [Cách dùng SSH key để push/pull](#cách-dùng-ssh-key-để-pushpull)
---
# GitHub Actions (tự động hóa quy trình phát triển phần mềm (CI/CD – Continuous Integration / Continuous Delivery).)
```bash
- Nói đơn giản: Nó cho phép bạn tạo các workflow (luồng công việc) để tự động chạy khi có sự kiện xảy ra trong repo (ví dụ: push code, tạo pull request, phát hành version…).
- GitHub Actions dùng để làm gì?
    + Build code tự động
    + Chạy test (unit test, integration test)
    + Deploy ứng dụng lên server / cloud
    + Kiểm tra lỗi, lint code
    + Tự động hóa các task khác (gửi email, tạo issue, update version…)
- Cách hoạt động (dễ hiểu)
    + GitHub Actions hoạt động dựa trên các thành phần:
        - Event (Sự kiện)
        Ví dụ: push, pull_request
        - Workflow
        File cấu hình .yml nằm trong thư mục .github/workflows/
        - Job
        Một nhóm các bước chạy trên máy ảo
        - Step
        Các lệnh cụ thể (run command hoặc dùng action có sẵn)
```
# Practices
## Cách dùng SSH key để push/pull
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
