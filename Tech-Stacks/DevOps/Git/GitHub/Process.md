- [Authentication (xác thực tài khoản)](#authentication-xác-thực-tài-khoản)
  - [PAT (Personal Acess Token - dùng để xác thực tài khoản)](#pat-personal-acess-token---dùng-để-xác-thực-tài-khoản)
  - [SSH (dùng để xác thực tài khoản sử dụng cặp khóa)](#ssh-dùng-để-xác-thực-tài-khoản-sử-dụng-cặp-khóa)
- [GitHub Actions (tự động hóa quy trình phát triển phần mềm (CI/CD – Continuous Integration / Continuous Delivery).)](#github-actions-tự-động-hóa-quy-trình-phát-triển-phần-mềm-cicd--continuous-integration--continuous-delivery)
- [Practices](#practices)
  - [Cách dùng SSH key để push/pull](#cách-dùng-ssh-key-để-pushpull)
- [Ask (câu hỏi)](#ask-câu-hỏi)
  - [PAT hay SSH an toàn hơn?](#pat-hay-ssh-an-toàn-hơn)
---
# Authentication (xác thực tài khoản)
##  PAT (Personal Acess Token - dùng để xác thực tài khoản)
```bash
PAT (Personal Access Token) là một chuỗi ký tự bí mật do GitHub cấp, dùng thay cho mật khẩu khi truy cập GitHub qua HTTPS.
    Ví dụ: ghp_3X4AbCdEfGhIjKlMnOpQrStUvWxYz123456

Khi push code: git push
    GitHub sẽ yêu cầu: Username:
        - Bạn nhập: your_username
        - Tiếp theo: Password:

    Bạn không nhập mật khẩu GitHub, mà nhập: ghp_xxxxxxxxxxxxxxxxx
```
**Cách hoạt động của PAT**
```bash
Git
↓
HTTPS
↓
Username + PAT
↓
GitHub xác thực
↓
Cho phép push/pull
```
**So sánh PAT và SSH**
```bash
PAT (Personal Access Token) và SSH đều là cách xác thực (authentication) khi Git làm việc với GitHub, nhưng cơ chế hoạt động rất khác nhau.
```
```bash
Tiêu chí	        PAT	                                SSH
Giao thức	        HTTPS	                            SSH
Xác thực bằng	    Token	                            Cặp khóa công khai/bí mật
URL repository	    https://github.com/user/repo.git	git@github.com:user/repo.git
Mức độ tiện lợi	    Dễ bắt đầu	                        Cần cấu hình ban đầu
Mức độ bảo mật	    Tốt nếu bảo vệ token	            Rất tốt nếu bảo vệ private key
Thường dùng	        CI/CD, script, máy dùng tạm	        Máy cá nhân, lập trình hằng ngày  
```
## SSH (dùng để xác thực tài khoản sử dụng cặp khóa)
**Ex**
```bash
id_ed25519       ← Private key (bí mật)
id_ed25519.pub   ← Public key (công khai)

Bạn:
    Tạo key trên máy.
    
    Upload public key lên GitHub.
    
    GitHub lưu public key.
-> Khi kết nối, GitHub kiểm tra chữ ký tạo từ private key trên máy bạn.
```
**Cách hoạt động của SSH**
```bash
Máy bạn
    Private Key
        │
        ▼
    Ký yêu cầu
        │
        ▼

GitHub
    Public Key
    ↓
    Xác minh
    ↓
    Cho phép truy cập
```
```bash
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
```
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
# Ask (câu hỏi)
## PAT hay SSH an toàn hơn?
**PAT**
```bash
Ưu điểm
    - Dễ tạo.
    - Dễ thu hồi (revoke).
    - Có thể giới hạn quyền (chỉ đọc, đọc/ghi, chỉ một số repository...).

Nhược điểm
    - Nếu token bị lộ: ghp_xxxxxxxxx. Người khác có thể dùng token đó đến khi bạn thu hồi hoặc token hết hạn.
```
**SSH**
```bash
Ưu điểm
    - Không gửi password hay token mỗi lần.
    - Private key không rời khỏi máy.
    - Thường được xem là an toàn và tiện lợi hơn cho phát triển hằng ngày.

Nhược điểm
    - Phải tạo key.
    - Phải thêm public key lên GitHub.
    - Nếu mất private key hoặc máy bị xâm nhập, bạn cần xóa public key khỏi GitHub và tạo cặp key mới.
```
**Khi nào nên dùng?**
```bash
Dùng PAT khi
    - Làm việc qua HTTPS.
    - Viết script hoặc CI/CD.
    - Không thể dùng SSH (ví dụ một số môi trường bị chặn cổng SSH).
    - Muốn cấp quyền có thời hạn hoặc phạm vi hẹp.

Dùng SSH khi
    - Làm việc trên máy cá nhân.
    - Push/Pull thường xuyên.
    - Không muốn nhập token.
    - Quản lý nhiều repository GitHub.
```