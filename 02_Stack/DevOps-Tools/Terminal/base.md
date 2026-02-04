- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
  - [1. Thao tác với Thư mục](#1-thao-tác-với-thư-mục)
  - [2. Thao tác với File](#2-thao-tác-với-file)
  - [Xem thời gian khởi động máy](#xem-thời-gian-khởi-động-máy)
  - [rmdir a](#rmdir-a)
- [sudo](#sudo)
---
# Cấu trúc thư mục
```bash
Terminal/
├── 01_file_directory_ops.md  # Thao tác File & Thư mục (mkdir, touch, ls, du, rm, cp, mv)
├── 02_system_disk_mgmt.md    # Thao tác với hệ thống (phần cứng, phần mềm)
└── 03_package_software.md    # Thao tác với phần mềm cài ngoài (cài, xóa, v.v)
```


## 1. Thao tác với Thư mục
- **Tạo thư mục tầng (Nested):** `mkdir -p path/to/dir`
- **Liệt kê file chi tiết (Size, Hidden):** `ls -lah`



## Xem thời gian khởi động máy

journalctl –list-boots

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
Tải git
    1. sudo apt update
    2. sudo apt install git
    3. git --version: Kiểm tra.
Cài đặt LibreOffice
    1. sudo apt update
    2. sudo apt install libreoffice
Cài đặt Visual Studio Code
    1. sudo apt update
    2. sudo apt install wget gpg
    3. wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
    4. sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
    5. sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] \
https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
    1. sudo apt update
    2. sudo apt install code
Cài đặt Python3.10
    1. sudo add-apt-repository ppa:deadsnakes/ppa
    2. sudo apt update
    3. sudo apt install python3.10
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
Lsblk
Trả về danh sách các ổ phân vùng.
Cú pháp:
    1. lsblk
    2. lsblk -f
