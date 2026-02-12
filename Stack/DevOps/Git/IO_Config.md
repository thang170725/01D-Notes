- [git config](#git-config)
- [git clone](#git-clone)
- [git pull](#git-pull)
---
# git config
**Syn**
```bash
1. –l (Xem toàn bộ thông tin cấu hình hiện tại)
2. git config –-global user.name “Le Duc Thang“ (Cấu hình tên của người dùng là Le Duc Thang)
3. git config –-global user.email “Le Duc Thang“ (Cấu hình email của người dùng là Le Duc Thang)
4. git config –-local user.name “Le Duc Thang“ (Cấu hình tên của người dùng là Le Duc Thang)
5. git config –-local user.email “Le Duc Thang“ (Cấu hình email của người dùng là Le Duc Thang)
6. git config –l -–global (Xem thông tin cấu hình của global)
7. git config –l –-local (Xem thông tin cấu hình của local)
```
# git clone 
```bash
Lệnh này giúp bạn sao chép toàn bộ mã nguồn, lịch sử thay đổi, nhánh, commit, và tất cả các file trong dự án về máy tính để làm việc trực tiếp.
```
**Syn**
```bash
1. Sao chép ma nguồn từ gitHub vào thư mục dev1
    git clone https://github.com/thang1707/lesson1.git dev1
2. clone nhánh cụ thể về máy tính
    git clone --branch khue --single-branch https://github.com/thang170725/elgamal.git
```
# git pull
```bash
- Lấy dữ liệu và hợp nhất (merge) những thay đổi đó vào nhánh hiện tại của bạn. 
- Lệnh này là sự kết hợp của 2 lệnh git fetch (lấy các thay đổi từ kho lưu trữ từ xa) và git merge (hợp nhất các thay đổi vào nhánh hiện tại)
```
**Syn**
```bash
1. pull từ nhánh main
    git pull origin main
2. git pull --no-rebase origin main
```