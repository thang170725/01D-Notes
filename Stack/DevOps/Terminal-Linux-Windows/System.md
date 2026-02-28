- [Display](#display)
  - [tree](#tree)
  - [du](#du)
  - [free](#free)
  - [df](#df)
- [clear](#clear)
- [sudo apt clean](#sudo-apt-clean)
- [sudo apt autoclean](#sudo-apt-autoclean)
- [Mount ổ cứng](#mount-ổ-cứng)
- [uptime](#uptime)
- [ac (Accounting)](#ac-accounting)
- [Sửa lỗi 2 màn](#sửa-lỗi-2-màn)
- [rm -rf ~/.cache/huggingface](#rm--rf-cachehuggingface)
- [GPU](#gpu)
  - [Kiểm tra GPU NVIDIA](#kiểm-tra-gpu-nvidia)
- [lsblk](#lsblk)
- [sudo](#sudo)
- [Powercfg /batteryreport](#powercfg-batteryreport)
---
# Display
```bash
Nhóm này dùng để cung cấp thông tin, mục đích là liệt kê.
```
## tree
```bash
xem cấu trúc thư mục hiện tại.
```
**Syn**
```bash
- tree -L 10    : liệt kê 10 cấp thư mục cây con
- tree -d -L 2  : liệt kê 2 cấp thư mục không liệt kê file
```
## du
```bash
Xem dung lương thư mục hoặc file.
```
**Syn**
```bash
du -sh: xem dung lượng thư mục hiện tại
```
## free
```bash
Lệnh này cho bạn cái nhìn tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm (cache).
```
## df
Xem dung lượng còn lại của ổ, -h là để hiển thị theo đơn vị dễ đọc.
```bash
1. df -h /
2. df -h /home
```
**Syn**
```bash
free -h
- -h: giúp hiển thị con số dưới dạng dễ đọc như GB, MB thay vì những dãy byte dài ngoằng
```
# clear
```bash
Xóa hết các dòng lệnh.
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
# Sửa lỗi 2 màn
```bash
1. prime-select query: Nếu là intel -> đây là lý do màn hình rời không hoạt động. On-demand là bạn đang ở chế độ GPU chuyển đổi theo yêu cầu (hybrid mode)
2. sudo prime-select nvidia
3. sudo reboot
```
# rm -rf ~/.cache/huggingface
# GPU
Kiểm tra secure boot
    1. mokutil --sb-state
    2. sudo dmesg | grep -i secure
Gỡ bỏ driver NVIDIA cũ
    1. sudo apt purge 'nvidia-*'
Cài driver NVIDIA
    1. ubuntu-drivers devices: Chạy lệnh sau để xem máy bạn đã cài driver gì.
    2. sudo apt update
    3. sudo apt install nvidia-driver-550: Cài driver cho nvidia nếu chưa cài.
    4. sudo reboot: Nếu chạy lệnh 2 thì phải chạy lệnh này ngay sau đó.
    5. Nếu lỗi kiểm tra secure Boot.
    6. lsmod | grep nvidia: Nếu không có dòng nào -> driver chưa được kernel load.
    7. 
## Kiểm tra GPU NVIDIA
```bash
1. nvidia-smi
2. lspci | grep -i vga: Kiểm tra tên gpu bất kỳ loại nào.
3. dpkg -L nvidia-utils-470 | grep nvidia-smi: Kiểm tra xem gói nằm ở đâu.
```
Cài đặt NVIDIA
    1. sudo apt update
    2. sudo apt install nvidia-smi
Thêm vào Path
    1. export PATH=/usr/bin:$PATH
    2. source ~/.bashrc
Cài CUDA Tookit
    1. nvcc --version: Kiểm tra gói cuda toolkit nào được cài chưa.
    2. sudo apt install nvidia-cuda-toolkit hoặc nên web cài
Thêm nvcc vào PATH
    1. nano ~/.bashrc
    2. export PATH=/usr/local/cuda-12.9/bin${PATH:+:${PATH}}: Thêm dòng này vào cuối file.
    3. export LD_LIBRARY_PATH=/usr/local/cuda-12.9/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}: thêm dòng này vào cuối file.
    4. Ctrl+O, Enter, Ctrl+X
    5. source ~/.bashrc
    6. nvcc --version
Cài cuDNN
Kiểm tra xem cuDNN đã được cài ở đâu
    1. dpkg -L libcudnn9-dev-cuda-12
    2. sudo find /usr -name cudnn_version.h
    3. sudo ln -s /usr/include/x86_64-linux-gnu/cudnn_version.h /usr/include/cudnn_version.h: Tạo liên kết mềm.
    4. cat /usr/include/cudnn_version.h | grep CUDNN_MAJOR -A 2: Kiểm tra
    5. 
Thêm cuDNN vào PATH
    1. source ~/.bashrc
    2. export PATH=/usr/local/cuda/bin:$PATH
    3. export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
    4. source ~/.bashrc
    5. sudo ldconfig: Cập nhật cache thư viện
lsmod | grep nvidia
# lsblk
```bash
Trả về danh sách các ổ phân vùng.
```
**Syn**
```bash
1. lsblk
2. lsblk -f
```
Keyboard
xset r off
Tắt repeat hoàn toàn, nhấn phím sẽ không lặp.
xset r on
Mở repeat.
# sudo
Cho phép sử dụng các task yêu cầu phải có quyền quản trị hoặc quyền root.
    • Sudo apt upgrade: tải các gói mới nhất về máy
    • sudo apt install software-properties-common -y: tải một ứng dựng nào đó
    • sudo add-apt-repository ppa:deadsnakes/ppa
    •  sudo apt clean: xóa cache tải về của apt 

Tải và sử dụng phần mềm gparted
    1. sudo apt update
    2. sudo apt install gparted: Tải ứng dụng phân vùng và format ổ mới.
    3. sudo gparted: Mở ứng dụng gparted.
    4. sudo update-grub: Cập nhật lại GRUB. (tùy chọn).



Cài portaudio
    1. sudo apt update
    2. sudo apt install portaudio19-dev python3-dev
    3. Vào môi trường ảo cài lại pyaudio (pip install pyaudio).
laalMic
Kiểm tra microphone có hoạt động không
    1. arecord - l: Nếu không có card nào hiện ra -> hệ thống không phát hiện được mic.
    2. arecord -D plughw:0,0 -f cd test.wav: Ghi âm.
    3. arecord -D hw:1,0 -f cd test.wav: Ghi âm.
    4. aplay test.wav: Chạy cái số 2. Sau 5 giây thì chạy lại cái này.
Mic bị gain quá cao (bị khuếch đại quá mức)
    1. alsamixer.
    2. Nhấn F4.
    3. Dùng phím mũi tên để giảm gian xuống thấp hơn.
    4. Esc để thoát.
Dkms status
mokutil –sb-state
Cài đặt espeak-ng
    1. sudo apt update
    2. sudo apt install espeak-ng
    3. espeak-ng “xin chào”
# Powercfg /batteryreport