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
├── 02_system_disk_mgmt.md    # Quản trị Hệ thống & Đĩa (mount, df, du, top, clear)
└── 03_package_software.md    # Cài đặt & Phần mềm (dpkg/deb, apt, update hệ thống)
```
**Chi tiết cách gộp nội dung**
```bash
1. 01_file_directory_ops.md (Quản lý File & Thư mục)
    + Đây là file bạn sẽ mở thường xuyên nhất.
    + Nội dung từ: mkdir.md, touch.md, ls.md.
    + Gợi ý thêm: Bạn nên cho lệnh rm (xóa file), cp (copy), mv (di chuyển) vào đây luôn.
2. 02_system_disk_mgmt.md (Hệ thống & Phần cứng)
    + Gom các lệnh tác động đến tài nguyên máy tính.
    + Nội dung từ: du.md (dung lượng), mount-disk.md, clear.md.
3. 03_package_software.md (Cài đặt & Cập nhật)
    + Gom các lệnh liên quan đến việc cài cắm tool.
    + Nội dung từ: file-deb.md, video.md (nếu đây là hướng dẫn cài tool quay phim/xử lý video), update.md.
    + Nội dung chính: Cách dùng dpkg, apt, hoặc cài đặt từ file .deb.
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
Video





pwd
Xem đường dẫn thư mục làm việc hiện tại.
cat file.txt
Liệt kê nội dung của file.txt
Cú pháp:
cat file.text


## rmdir a
xóa thư mục a, thư mục a phải là thư mục trống.

Gỡ, xóa phần mềm, …
    1. dpkg -l | grep chrome: Tìm phần mềm đã cài.
    2. sudo apt remove google-chrome-stable: Gỡ phần mềm.
    3. sudo apt purge google-chrome-stable: Nếu muốn gỡ sạch hơn.
    4. sudo apt autoremove: Dọn lại hệ thống (xóa gói đã cài nhưng không cần nữa).
    5. sudo apt clean: Xóa cache tải về của apt.
    6. sudo apt autoclean: Nếu muốn dọn triệt để hơn (chỉ giữ lại vài file).
Sửa lổi
Sửa lỗi 2 màn
    1. prime-select query: Nếu là intel -> đây là lý do màn hình rời không hoạt động. On-demand là bạn đang ở chế độ GPU chuyển đổi theo yêu cầu (hybrid mode)
    2. sudo prime-select nvidia
    3. sudo reboot
# sudo
Cho phép sử dụng các task yêu cầu phải có quyền quản trị hoặc quyền root.
    • Sudo apt upgrade: tải các gói mới nhất về máy
    • sudo apt install software-properties-common -y: tải một ứng dựng nào đó
    • sudo add-apt-repository ppa:deadsnakes/ppa
    •  sudo apt clean: xóa cache tải về của apt 
Cài bộ gõ tiếng việt
    1. sudo add-apt-repository ppa:bamboo-engine/ibus-bamboo: Thêm PPA chính thức của Bamboo.
    2. sudo apt install software-properties-common: Nếu máy chưa có add-apt-repository thì cài thêm cái này.
    3. dpkg -l | grep bamboo: Kiểm tra xem đã cài bộ cài tiếng việt chưa.
    4. sudo apt update
    5. sudo apt install ibus-bamboo: Cài đặt ibus-bamboo.
    6. ibus restart: Thiết lập để sử dụng.
    7. Sau đó vào settings -> Region & Lanuage -> …
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
GPU
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
Kiểm tra GPU NVIDIA
    1. nvidia-smi
    2. lspci | grep -i vga: Kiểm tra tên gpu bất kỳ loại nào.
    3. dpkg -L nvidia-utils-470 | grep nvidia-smi: Kiểm tra xem gói nằm ở đâu.
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
