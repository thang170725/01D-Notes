- [clear](#clear)
- [tree](#tree)
- [du](#du)
- [free](#free)
- [df](#df)
- [sudo apt clean](#sudo-apt-clean)
- [sudo apt autoclean](#sudo-apt-autoclean)
- [Mount ổ cứng](#mount-ổ-cứng)
- [uptime](#uptime)
- [ac (Accounting)](#ac-accounting)
---
# clear
```bash
Xóa hết các dòng lệnh.
```
# tree
xem cấu trúc thư mục hiện tại.
```bash
tree -L 10
```
# du
```bash
Xem dung lương thư mục hoặc file.
```
**Syn**
```bash
du -sh: xem dung lượng thư mục hiện tại
```
# free
Lệnh này cho bạn cái nhìn tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm (cache).
```bash
free -h
- -h: giúp hiển thị con số dưới dạng dễ đọc như GB, MB thay vì những dãy byte dài ngoằng
```

# df
Xem dung lượng còn lại của ổ, -h là để hiển thị theo đơn vị dễ đọc.
```bash
1. df -h /
2. df -h /home
```

# sudo apt clean
```bash
Xóa toàn bộ file .deb đã tải
```
# sudo apt autoclean
```bash
Chỉ xóa các gói cũ, không còn dùng.
```
2️⃣ Xóa package không còn cần thiết
bash
Copy code
sudo apt autoremove
Xóa dependency thừa sau khi gỡ phần mềm.

👉 Thường nên chạy combo:

bash
Copy code
sudo apt autoremove --purge
sudo apt clean
3️⃣ Dọn log hệ thống (journal)
Kiểm tra log đang chiếm bao nhiêu:

bash
Copy code
journalctl --disk-usage
Chỉ giữ log 7 ngày:

bash
Copy code
sudo journalctl --vacuum-time=7d
Hoặc giới hạn dung lượng (ví dụ 500MB):

bash
Copy code
sudo journalctl --vacuum-size=500M
4️⃣ Dọn cache người dùng
bash
Copy code
rm -rf ~/.cache/*
⚠️ Lệnh này chỉ xóa cache, không ảnh hưởng dữ liệu cá nhân.

5️⃣ Nếu có dùng Docker (rất hay đầy disk)
Kiểm tra:

bash
Copy code
docker system df
Dọn rác Docker:

bash
Copy code
docker system prune -a
⚠️ Sẽ xóa image, container không dùng.

6️⃣ Nếu dùng Snap
Xem snap chiếm dung lượng:

bash
Copy code
du -h /var/lib/snapd/snaps | sort -h
Xóa snap version cũ:

bash
Copy code
sudo snap set system refresh.retain=2
sudo snap remove --purge <tên_snap>
7️⃣ Tìm thư mục “ăn dung lượng”
Rất hữu ích:

bash
Copy code
sudo du -h / --max-depth=1 2>/dev/null | sort -h
Hoặc dùng công cụ trực quan:

bash
Copy code
sudo apt install ncdu
sudo ncdu /
👉 Gợi ý nhanh
Nếu bạn chỉ muốn dọn rác cơ bản, an toàn, cứ chạy:

bash
Copy code
sudo apt autoremove --purge
sudo apt clean
sudo journalctl --vacuum-time=7d
# Mount ổ cứng
**Step**
```bash
1. sudo apt install nfs-common
2. sudo apt install cifs-utils
3. sudo apt install ntfs-sg
4. sudo ntfsfix -b -d /dev/nvme1n1p4
```
# uptime
```bash
Xem thời gian bắt đầu mở máy tính.
```
**Ex**
```bash
thang@PhatToNhuLai:~$ uptime -s
2025-08-14 15:29:59
```
# ac (Accounting) 
```bash
- Lệnh ac sẽ cho biết tổng số giờ ma người dùng đã đăng nhập.
```
**Syn**
```bash
1. Cài đặt nếu chưa có:
    1. sudo apt install acct   # Ubuntu/Debian
    2. sudo systemctl start acct
    3. sudo systemctl enable acct
2. ac -d    # Aug 14 total      5.40
3. ac -p    # total      569.53
```