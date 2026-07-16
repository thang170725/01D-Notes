- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [uptime](#uptime)
  - [ac (Accounting)](#ac-accounting)
  - [tree](#tree)
  - [du](#du)
- [RAM](#ram)
  - [free (tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm)](#free-tổng-quan-nhất-về-dung-lượng-ram-tổng-dung-lượng-đã-dùng-còn-trống-và-bộ-nhớ-đệm)
  - [df (Xem dung lượng còn lại của ổ)](#df-xem-dung-lượng-còn-lại-của-ổ)
- [Service](#service)
  - [systemctl \& sudo systemctl (Quản lý các service)](#systemctl--sudo-systemctl-quản-lý-các-service)
    - [status (Kiểm tra trạng thái service có đang chạy không)](#status-kiểm-tra-trạng-thái-service-có-đang-chạy-không)
    - [sudo lsof (Kiểm tra xem port nào đang bị sử dụng)](#sudo-lsof-kiểm-tra-xem-port-nào-đang-bị-sử-dụng)
    - [ss -tulpn | grep (Kiểm tra xem port nào đang bị sử dụng)](#ss--tulpn--grep-kiểm-tra-xem-port-nào-đang-bị-sử-dụng)
    - [systemctl list-units (Dùng để: liệt kê các service đang hoạt động (hoặc được systemd quản lý))](#systemctl-list-units-dùng-để-liệt-kê-các-service-đang-hoạt-động-hoặc-được-systemd-quản-lý)
    - [start (Mở lại một service đã Stop)](#start-mở-lại-một-service-đã-stop)
    - [sudo systemctl stop (Dừng một service đang chạy)](#sudo-systemctl-stop-dừng-một-service-đang-chạy)
    - [sudo systemctl disable (Dùng khi muốn tắt hẳn service)](#sudo-systemctl-disable-dùng-khi-muốn-tắt-hẳn-service)
  - [Powercfg /batteryreport (Windows)](#powercfg-batteryreport-windows)
- [Create \& Config (Tạo \& cấu hình)](#create--config-tạo--cấu-hình)
- [Remove \& Close (Nhóm xóa \& dừng)](#remove--close-nhóm-xóa--dừng)
  - [clear](#clear)
  - [sudo apt clean](#sudo-apt-clean)
  - [sudo apt autoclean](#sudo-apt-autoclean)
  - [sudo apt autoremove](#sudo-apt-autoremove)
- [Mount disk (mount ổ cứng)](#mount-disk-mount-ổ-cứng)
- [Sửa lỗi 2 màn](#sửa-lỗi-2-màn)
- [rm -rf ~/.cache/huggingface](#rm--rf-cachehuggingface)
- [GPU](#gpu)
  - [VRAM (giống như bàn làm việc của GPU)](#vram-giống-như-bàn-làm-việc-của-gpu)
  - [CUDA Toolkit](#cuda-toolkit)
  - [Check (kiểm tra)](#check-kiểm-tra)
    - [nvidia-smi](#nvidia-smi)
      - [Các bước kiểm tra GPU NVIDIA](#các-bước-kiểm-tra-gpu-nvidia)
    - [Kiểm tra secure boot](#kiểm-tra-secure-boot)
  - [Install (cài đặt)](#install-cài-đặt)
    - [Các bước cài driver NVIDIA](#các-bước-cài-driver-nvidia)
    - [Các bước cài CUDA Tookit](#các-bước-cài-cuda-tookit)
    - [Các bước cài cuDNN](#các-bước-cài-cudnn)
- [Remove (xóa, gỡ bỏ)](#remove-xóa-gỡ-bỏ)
  - [Gỡ bỏ driver NVIDIA cũ](#gỡ-bỏ-driver-nvidia-cũ)
- [lsblk](#lsblk)
- [Keyboard](#keyboard)
  - [Remove \& Stop (Xóa, Tắt, Dừng)](#remove--stop-xóa-tắt-dừng)
    - [xset r off](#xset-r-off)
  - [Create \& Open (Tạo, Mở)](#create--open-tạo-mở)
    - [xset r on](#xset-r-on)
- [Microphone](#microphone)
  - [Check (Kiểm tra)](#check-kiểm-tra-1)
    - [Các bước kiểm tra microphone có hoạt động không](#các-bước-kiểm-tra-microphone-có-hoạt-động-không)
    - [Mic bị gain quá cao (bị khuếch đại quá mức)](#mic-bị-gain-quá-cao-bị-khuếch-đại-quá-mức)
- [Powershell chặn việc chạy script](#powershell-chặn-việc-chạy-script)
  - [Get-ExecutionPolicy -List (kiểm tra chính sách hiện tại)](#get-executionpolicy--list-kiểm-tra-chính-sách-hiện-tại)
  - [Set-ExecutionPolicy -Scope CurrentUser RemoteSigned](#set-executionpolicy--scope-currentuser-remotesigned)
---
# Display (Nhóm cung cấp thông tin)
## uptime
```bash
Xem thời gian bắt đầu mở máy tính.
```
**Ex**
```bash
thang@PhatToNhuLai:~$ uptime -s
2025-08-14 15:29:59
```
## ac (Accounting) 
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
# RAM
## free (tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm)
**Syn**
```bash
free -h
- -h: giúp hiển thị con số dưới dạng dễ đọc như GB, MB thay vì những dãy byte dài ngoằng
```
## df (Xem dung lượng còn lại của ổ)
```bash
1. df -h / # -h là để hiển thị theo đơn vị dễ đọc.
2. df -h /home
```
# Service 
## systemctl & sudo systemctl (Quản lý các service)
**Ex**
```bash
1. systemctl list-units --type=service
    + Hiển thị các service đang active
2. systemctl list-unit-files --type=service
    + Hiển thị các service kể cả đang tắt
3. systemctl list-units --type=service --state=running
    + Chỉ xem service đang chạy
```
###  status (Kiểm tra trạng thái service có đang chạy không)
```bash
Nó dùng để:
    - Xem PID
    - Xem log gần nhất
    - Xem có lỗi không
    - Xem service có tự start khi boot không
```
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe/frontend$ sudo systemctl status 1798

# ● mariadb.service - MariaDB 10.11.13 database server
#      Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; preset: enabled)
#      Active: active (running) since Wed 2026-03-25 20:34:16 +07; 42min ago
#        Docs: man:mariadbd(8)
#              https://mariadb.com/kb/en/library/systemd/
#     Process: 1630 ExecStartPre=/usr/bin/install -m 755 -o mysql -g root -d /var/run/mysqld (code=exited, status=0/SU>
#     Process: 1668 ExecStartPre=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/S>
#     Process: 1685 ExecStartPre=/bin/sh -c [ ! -e /usr/bin/galera_recovery ] && VAR= ||   VAR=`/usr/bin/galera_recove>
#     Process: 1936 ExecStartPost=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/>
#     Process: 1938 ExecStartPost=/etc/mysql/debian-start (code=exited, status=0/SUCCESS)
#    Main PID: 1798 (mariadbd)
#      Status: "Taking your SQL requests now..."
#       Tasks: 9 (limit: 123309)
#      Memory: 112.6M (peak: 117.5M)
#         CPU: 581ms
#      CGroup: /system.slice/mariadb.service
#              └─1798 /usr/sbin/mariadbd
```
### sudo lsof (Kiểm tra xem port nào đang bị sử dụng)
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe/frontend$ sudo lsof -i :3306

# COMMAND   PID  USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
# mariadbd 1798 mysql   34u  IPv4  20838      0t0  TCP localhost:mysql (LISTEN)
```
### ss -tulpn | grep (Kiểm tra xem port nào đang bị sử dụng)
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe/frontend$ ss -tulpn | grep 3306
# tcp   LISTEN 0      80                               127.0.0.1:3306       0.0.0.0:*
```
### systemctl list-units (Dùng để: liệt kê các service đang hoạt động (hoặc được systemd quản lý))
**Ex**
```bash
systemctl list-units --type=service | grep -E 'mysql|mariadb'

- systemctl list-units --type=service
    + systemctl: công cụ quản lý service trong Linux (systemd)
    + list-units: liệt kê các “unit” (đơn vị hệ thống)
    + --type=service: chỉ lấy service
=> Kết quả: danh sách các service đang active (đang chạy)
- | (pipe): Chuyển output của lệnh bên trái sang lệnh bên phải
    + grep -E 'mysql|mariadb'
    + grep: tìm kiếm text
    + -E: cho phép dùng regex (biểu thức chính quy)
    + 'mysql|mariadb': tìm dòng chứa mysql HOẶC mariadb
=> Hiểu đơn giản: “Cho tôi xem các service đang chạy có liên quan đến MySQL hoặc MariaDB”
```
### start (Mở lại một service đã Stop)
**Syn**
```bash
sudo systemctl start <service>
```
### sudo systemctl stop (Dừng một service đang chạy)
```bash
Khi chạy lệnh này, systemd sẽ:
    + Gửi tín hiệu dừng (SIGTERM)
    + Tắt tiến trình của service
    + Giải phóng tài nguyên (RAM, CPU, file lock, port…)
```
**Syn**
```bash
sudo systemctl stop <tên-service>
```
### sudo systemctl disable (Dùng khi muốn tắt hẳn service)
**Syn**
```bash
sudo systemctl disable <service>
```
## Powercfg /batteryreport (Windows)
# Create & Config (Tạo & cấu hình)
# Remove & Close (Nhóm xóa & dừng)
## clear
```bash
Xóa hết các dòng lệnh.
```
## sudo apt clean
```bash
Xóa toàn bộ file .deb đã tải
```
## sudo apt autoclean
```bash
Chỉ xóa các gói cũ, không còn dùng.
```
## sudo apt autoremove
```bash
Xóa dependency thừa sau khi gỡ phần mềm.
```
# Mount disk (mount ổ cứng)
**Step**
```bash
1. sudo apt install nfs-common
2. sudo apt install cifs-utils
3. sudo apt install ntfs-sg
4. sudo ntfsfix -b -d /dev/nvme1n1p4
```
# Sửa lỗi 2 màn
```bash
1. prime-select query: Nếu là intel -> đây là lý do màn hình rời không hoạt động. On-demand là bạn đang ở chế độ GPU chuyển đổi theo yêu cầu (hybrid mode)
2. sudo prime-select nvidia
3. sudo reboot
```
# rm -rf ~/.cache/huggingface
# GPU
## VRAM (giống như bàn làm việc của GPU)
**Tác động của VRAM đối với train AI**
```bash
Khi train model, VRAM phải chứa:
    Model Weights
    +
    Activations
    +
    Gradients
    +
    Optimizer States

Giống như: Bàn làm việc
┌─────────────────┐
│ Tài liệu        │ ← Weights
│ Giấy nháp       │ ← Activations
│ Kết quả tính    │ ← Gradients
│ Sổ ghi chú      │ ← Optimizer
└─────────────────┘
```
## CUDA Toolkit
```bash
- Nó là bộ thư viện lập trình (compiler, headers...) để bạn code và chạy trực tiếp trên Ubuntu.
```
## Check (kiểm tra)
### nvidia-smi
```bash
thang@PhatToNhuLai:~$ nvidia-smi
Sun Mar 22 17:22:42 2026       
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 570.211.01             Driver Version: 570.211.01     CUDA Version: 12.8     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3050 ...    Off |   00000000:01:00.0 Off |                  N/A |
| N/A   64C    P3             16W /   60W |     327MiB /   4096MiB |     25%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+
                                                                                         
+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A            3111      G   /usr/lib/xorg/Xorg                      165MiB |
|    0   N/A  N/A            3478      G   /usr/bin/gnome-shell                     44MiB |
|    0   N/A  N/A            4231      G   ...rack-uuid=3190708988185955192         23MiB |
|    0   N/A  N/A            4554      G   /usr/share/cursor/cursor                 62MiB |
+-----------------------------------------------------------------------------------------+

- Driver Version: 570.211.01    : Đây là phiên bản driver rất mới. Nó là "cầu nối" phần cứng.
- CUDA Version: 12.8            : Đây là điểm gây hiểu lầm nhất.
    + Ý nghĩa: Đây KHÔNG PHẢI là phiên bản CUDA bạn đã cài. Đây là phiên bản CUDA cao nhất mà Driver này có thể hỗ trợ.
- GPU Name: NVIDIA GeForce RTX 3050 (4096MiB):
    + Bạn có 4GB VRAM. Đây là thông số quan trọng nhất khi chọn Model AI.
    + Lời khuyên: Với 4GB, bạn sẽ chạy cực tốt các dòng YOLO (v8, v10, v11), các model MediaPipe, hoặc các LLM siêu nhỏ (như Phi-3 mini) nếu biết cách tối ưu. Đừng cố chạy các model quá nặng như Llama-3 70B vì sẽ bị báo lỗi Out of Memory (OOM).
```
#### Các bước kiểm tra GPU NVIDIA
```bash
1. xem driver gpu
    nvidia-smi
2. Kiểm tra tên gpu bất kỳ loại nào.
    lspci | grep -i vga                      
3. Kiểm tra xem gói nằm ở đâu.
    dpkg -L nvidia-utils-470 | grep nvidia-smi
```
### Kiểm tra secure boot
```bash
1. mokutil --sb-state
2. sudo dmesg | grep -i secure
```
## Install (cài đặt)
### Các bước cài driver NVIDIA
```bash
1. Chạy lệnh sau để xem máy bạn đã cài driver gì.
    ubuntu-drivers devices: 
2. sudo apt update
3. Cài driver cho nvidia nếu chưa cài.
    sudo apt install nvidia-driver-550
4. Nếu chạy lệnh 2 thì phải chạy lệnh này ngay sau đó.
    sudo reboot
5. Nếu lỗi => kiểm tra secure Boot.
6. Nếu không có dòng nào -> driver chưa được kernel load.
    lsmod | grep nvidia 
```
### Các bước cài CUDA Tookit
```bash
    1. nvcc --version: Kiểm tra gói cuda toolkit nào được cài chưa.
    2. sudo apt install nvidia-cuda-toolkit hoặc nên web cài
Thêm nvcc vào PATH
    1. nano ~/.bashrc
    2. export PATH=/usr/local/cuda-12.9/bin${PATH:+:${PATH}}: Thêm dòng này vào cuối file.
    3. export LD_LIBRARY_PATH=/usr/local/cuda-12.9/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}: thêm dòng này vào cuối file.
    4. Ctrl+O, Enter, Ctrl+X
    5. source ~/.bashrc
    6. nvcc --version
```
Cài đặt NVIDIA
    1. sudo apt update
    2. sudo apt install nvidia-smi
Thêm vào Path
    1. export PATH=/usr/bin:$PATH
    2. source ~/.bashrc

### Các bước cài cuDNN
```bash
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
```
# Remove (xóa, gỡ bỏ)
## Gỡ bỏ driver NVIDIA cũ
```bash
1. sudo apt purge 'nvidia-*'
```
# lsblk
```bash
Trả về danh sách các ổ phân vùng.
```
**Syn**
```bash
1. lsblk
2. lsblk -f
```
# Keyboard
## Remove & Stop (Xóa, Tắt, Dừng)
### xset r off
```bash
Tắt repeat hoàn toàn, nhấn phím sẽ không lặp.
```
## Create & Open (Tạo, Mở)
### xset r on
```bash
Mở repeat.
```
# Microphone
## Check (Kiểm tra)
### Các bước kiểm tra microphone có hoạt động không
```bash
1. arecord - l: Nếu không có card nào hiện ra -> hệ thống không phát hiện được mic.
2. arecord -D plughw:0,0 -f cd test.wav: Ghi âm.
3. arecord -D hw:1,0 -f cd test.wav: Ghi âm.
4. aplay test.wav: Chạy cái số 2. Sau 5 giây thì chạy lại cái này.
```
### Mic bị gain quá cao (bị khuếch đại quá mức)
```bash
1. alsamixer.
2. Nhấn F4.
3. Dùng phím mũi tên để giảm gian xuống thấp hơn.
4. Esc để thoát.
```
# Powershell chặn việc chạy script
## Get-ExecutionPolicy -List (kiểm tra chính sách hiện tại) 
## Set-ExecutionPolicy -Scope CurrentUser RemoteSigned