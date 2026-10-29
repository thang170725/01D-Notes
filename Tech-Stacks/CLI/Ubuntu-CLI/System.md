- [uptime (Xem thời gian bắt đầu mở máy tính)](#uptime-xem-thời-gian-bắt-đầu-mở-máy-tính)
- [ac (Accounting) (cho biết tổng số giờ ma người dùng đã đăng nhập)](#ac-accounting-cho-biết-tổng-số-giờ-ma-người-dùng-đã-đăng-nhập)
- [tree (xem cấu trúc thư mục hiện tại)](#tree-xem-cấu-trúc-thư-mục-hiện-tại)
  - [du (Xem dung lương thư mục hoặc file)](#du-xem-dung-lương-thư-mục-hoặc-file)
- [free (tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm)](#free-tổng-quan-nhất-về-dung-lượng-ram-tổng-dung-lượng-đã-dùng-còn-trống-và-bộ-nhớ-đệm)
- [df (Xem dung lượng còn lại của ổ)](#df-xem-dung-lượng-còn-lại-của-ổ)
- [systemctl | sudo systemctl (Quản lý các service)](#systemctl--sudo-systemctl-quản-lý-các-service)
    - [status (Kiểm tra trạng thái service có đang chạy không)](#status-kiểm-tra-trạng-thái-service-có-đang-chạy-không)
- [lsof | sudo lsof (Kiểm tra xem port nào đang bị sử dụng)](#lsof--sudo-lsof-kiểm-tra-xem-port-nào-đang-bị-sử-dụng)
- [ss (Xem port nào đang mớ)](#ss-xem-port-nào-đang-mớ)
  - [ss -lntp (xem tất cả các port đang ở trạng thái lắng nghe)](#ss--lntp-xem-tất-cả-các-port-đang-ở-trạng-thái-lắng-nghe)
- [nc (kiểm tra một port từ máy khác)](#nc-kiểm-tra-một-port-từ-máy-khác)
- [ps — tìm tiến trình theo cách có kiểm soát](#ps--tìm-tiến-trình-theo-cách-có-kiểm-soát)
- [kill (dừng port đang chạy)](#kill-dừng-port-đang-chạy)
- [ip (kiểm tra IP và routing)](#ip-kiểm-tra-ip-và-routing)
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
  - [Cài đặt NVIDIA](#cài-đặt-nvidia)
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
- [id và namei — tìm nguyên nhân Permission denied](#id-và-namei--tìm-nguyên-nhân-permission-denied)
---
# uptime (Xem thời gian bắt đầu mở máy tính)
**Ex**
```bash
thang@PhatToNhuLai:~$ uptime -s
2025-08-14 15:29:59
```
# ac (Accounting) (cho biết tổng số giờ ma người dùng đã đăng nhập)
**Syn**
```bash
1. Cài đặt nếu chưa có:
    1. sudo apt install acct   # Ubuntu/Debian
    2. sudo systemctl start acct
    3. sudo systemctl enable acct
2. ac -d    # Aug 14 total      5.40
3. ac -p    # total      569.53
```
# tree (xem cấu trúc thư mục hiện tại)
**Syn**
```bash
- tree -L 10    : liệt kê 10 cấp thư mục cây con
- tree -d -L 2  : liệt kê 2 cấp thư mục không liệt kê file
```
## du (Xem dung lương thư mục hoặc file)

**Ex: xem dung lượng thư mục hiện tại**
```bash
du -sh
```
# free (tổng quan nhất về dung lượng RAM tổng, dung lượng đã dùng, còn trống và bộ nhớ đệm)
**Ex**
```bash
free -h # -h: giúp hiển thị con số dưới dạng dễ đọc như GB, MB thay vì những dãy byte dài ngoằng
#                total   used   free  shared  buff/cache  available
# Mem:             16Gi    9Gi   1.2Gi   500Mi       5.8Gi       6Gi
# Swap:             2Gi    0Gi     2Gi
```
# df (Xem dung lượng còn lại của ổ)
```bash
1. df -h / # -h là để hiển thị theo đơn vị dễ đọc.
2. df -h /home
```
# systemctl | sudo systemctl (Quản lý các service)
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
# lsof | sudo lsof (Kiểm tra xem port nào đang bị sử dụng)
```bash
lsof là viết tắt của List Open Files. Trên Linux, socket mạng cũng được xem là một dạng tài nguyên mở, nên lệnh này có thể giúp tìm process sử dụng port
```
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe/frontend$ sudo lsof -i :3306

# COMMAND   PID  USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
# mariadbd 1798 mysql   34u  IPv4  20838      0t0  TCP localhost:mysql (LISTEN)
```
# ss (Xem port nào đang mớ)
```bash
ss dùng để kiểm tra socket mạng, kết nối TCP/UDP và các port đang được lắng nghe. Đây là công cụ chẩn đoán mạng rất hữu ích trên Linux.
```
**Khi nào dùng?**
```bash
- Chạy ứng dụng Python nhưng không biết ứng dụng có mở port hay chưa.
- Gặp lỗi Address already in use.
- Muốn biết port 8000, 5432, 8080 có đang được sử dụng không.
```
**Syn**
```bash
ss [options] [filter]

- Input:
    + option:
        -l: Chỉ hiển thị socket đang lắng nghe
        -n: Hiển thị địa chỉ và port dạng số
        -t: TCP
        -p: Hiển thị process liên quan nếu có quyền
```
## ss -lntp (xem tất cả các port đang ở trạng thái lắng nghe)
**Ex**
```bash
ss -lntp

# State  Recv-Q Send-Q Local Address:Port  Peer Address:Port Process
# LISTEN 0      2048   0.0.0.0:8000        0.0.0.0:*     users:(("python",pid=2451,fd=3))
# LISTEN 0      4096   0.0.0.0:5432        0.0.0.0:*     users:(("postgres",pid=812,fd=7))
```
**Ex2: chỉ kiểm tra port 8000**
```bash
ss -lntp 'sport = :8000'
```
-tulpn | grep (Kiểm tra xem port nào đang bị sử dụng)
**Ex**
```bash
(sr) thang@PhatToNhuLai:~/workspace/Smart-Recipe/frontend$ ss -tulpn | grep 3306
# tcp   LISTEN 0      80                               127.0.0.1:3306       0.0.0.0:*
```
# nc (kiểm tra một port từ máy khác)
ú pháp:
nc -vz HOST PORT


Ví dụ:
nc -vz 192.168.9.56 5432


Output thành công minh họa:
Connection to 192.168.9.56 5432 port [tcp/postgresql] succeeded!


Output thất bại có thể là:
nc: connect to 192.168.9.56 port 5432 (tcp) failed: Connection refused
# ps — tìm tiến trình theo cách có kiểm soát
Ví dụ xem các process thuộc tài khoản hiện tại:
ps -u "$USER" -o pid,ppid,%cpu,%mem,stat,etime,cmd


Các cột:
- PID: ID của process.
- PPID: ID của process cha.
- %CPU, %MEM: mức sử dụng CPU và RAM.
- STAT: trạng thái process.
- ETIME: thời gian đã chạy.
- CMD: lệnh khởi chạy.
Tìm tất cả process liên quan đến Uvicorn:
pgrep -af uvicorn


Output minh họa:
2451 /home/thang/project/.venv/bin/python ... uvicorn main:app


Khác biệt quan trọng:
- ps: xem thông tin chi tiết của process.
- pgrep: tìm PID theo tên hoặc pattern, đặc biệt tiện khi cần tìm nhanh một ứng dụng.
# kill (dừng port đang chạy)
**Ex**
```bash
kill -TERM 2451
```
kill — gửi tín hiệu cho process
kill không đơn thuần là “giết process”; nó gửi một signal để yêu cầu process thực hiện hành động.
kill -TERM 2451


TERM yêu cầu process kết thúc một cách bình thường, để ứng dụng có cơ hội đóng kết nối hoặc giải phóng tài nguyên.

Kiểm tra signal:
kill -l


Một số signal thường gặp:
Signal	Ý nghĩa
TERM (15)	Yêu cầu kết thúc bình thường
INT (2)	Tương tự thao tác ngắt bằng bàn phím
HUP (1)	Thường được ứng dụng dùng để reload cấu hình
KILL (9)	Buộc kernel kết thúc process, không thể bắt hoặc bỏ qua

Để dừng một ứng dụng, ưu tiên TERM trước. KILL không cho ứng dụng cơ hội tự dọn dẹp.
# ip (kiểm tra IP và routing)
Thay vì chỉ xem địa chỉ IP bằng một lệnh đơn giản, hãy học cách kiểm tra cấu hình mạng thực tế.
ip -br addr


Output minh họa:
lo       UNKNOWN  127.0.0.1/8 ::1/128
eth0     UP       192.168.1.20/24


Xem đường đi mạng mặc định:
ip route


Output minh họa:
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link


Kiểm tra hệ thống định tuyến để đi tới một server:
ip route get 192.168.9.56


Lệnh này giúp xác định interface và địa chỉ nguồn mà Linux dự định sử dụng để kết nối tới IP đích.
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
## Cài đặt NVIDIA
```bash
1. sudo apt update
2. sudo apt install nvidia-smi

Thêm vào Path
    1. export PATH=/usr/bin:$PATH
    2. source ~/.bashrc
```
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
Trong Ubuntu, lệnh grep dùng để tìm kiếm các dòng có chứa một từ khóa hoặc khớp với một mẫu nhất định trong văn bản, file hoặc đầu ra của lệnh khác.

Ví dụ, khi bạn chạy:
history | grep superset


Bạn đang tìm lại những lệnh đã chạy trước đó có chứa từ superset.
1. Hiểu lệnh grep qua ví dụ
Giả sử bạn có danh sách lịch sử lệnh như sau:
101  ls
102  cd /home/user
103  git clone https://github.com/example/superset.git
104  docker ps
105  cd superset
106  docker compose up -d


Nếu chạy:
history | grep superset


Kết quả có thể là:
103  git clone https://github.com/example/superset.git
105  cd superset


grep superset lọc ra những dòng có chứa từ superset, còn các dòng khác bị loại bỏ.

Hãy hiểu đơn giản:
- history: hiển thị lịch sử các lệnh bạn đã chạy.
- |: chuyển đầu ra của lệnh bên trái sang đầu vào của lệnh bên phải.
- grep superset: chỉ giữ lại các dòng chứa từ superset.
Cách hoạt động
history

Toàn bộ lịch sử lệnh

| — chuyển dữ liệu

grep superset

Lọc dòng chứa từ khóa


Chỉ hiển thị dòng phù hợp


2. Lệnh history | grep clone dùng để làm gì?
Lệnh này tìm lại các lệnh có chứa từ clone trong lịch sử terminal.
history | grep clone


Ví dụ kết quả:
25  git clone https://github.com/user/project.git
48  git clone -b develop https://github.com/user/api.git
72  git clone git@github.com:user/backend.git


Lệnh này đặc biệt hữu ích khi bạn quên chính xác câu lệnh đã sử dụng trước đó, chẳng hạn:
- Bạn đã clone repository nào?
- Bạn đã dùng URL HTTPS hay SSH?
- Bạn đã clone nhánh develop bằng lệnh nào?
- Trước đây bạn đã chạy lệnh cài đặt hoặc khởi động một dịch vụ ra sao?
Thay vì nhớ lại hoặc gõ lại lệnh từ đầu, bạn có thể tìm trong lịch sử.
3. Các cách sử dụng grep phổ biến
Bạn có thể chọn từng ví dụ để xem cách áp dụng.
history | grep supersetTìm tất cả lệnh trong history có chứa superset.Khi dùng: Khi muốn tìm lại lệnh đã thao tác với Superset.history | grep -i supersethistory | grep -n clonehistory | grep -E 'clone|pull|fetch'grep -n 'ERROR' app.loggrep -r 'superset' .history | grep -v sudo Sao chép lệnh
Lưu ý: Với grep -r, dấu . nghĩa là thư mục hiện tại. Hãy chạy lệnh tại thư mục dự án mà bạn muốn tìm kiếm.
4. Khi nào nên sử dụng grep?
Trong thực tế, bạn sẽ thường dùng grep trong những trường hợp sau:
Tình huống	Ví dụ
Tìm lệnh đã chạy	history \| grep docker
Tìm lỗi trong log	grep 'ERROR' app.log
Tìm cấu hình trong file	grep 'PORT' .env
Tìm chuỗi trong mã nguồn	grep -r 'DATABASE_URL' .
Tìm nhiều từ khóa	history \| grep -E 'clone\|pull'

Một số tùy chọn rất đáng nhớ:
- -i: không phân biệt chữ hoa/chữ thường.
- -n: hiển thị số dòng trong file hoặc đầu ra.
- -r: tìm đệ quy trong thư mục con.
- -v: lấy những dòng không khớp.
- -E: hỗ trợ biểu thức chính quy mở rộng, ví dụ dùng | để tìm nhiều từ khóa.
5. Phân biệt grep, history và |
Ba thành phần này có nhiệm vụ khác nhau:
Thành phần	Chức năng
history	Xem lịch sử các lệnh đã chạy
grep	Tìm và lọc dòng theo từ khóa
\|	Chuyển đầu ra của lệnh trước sang lệnh sau

Bạn có thể kết hợp grep với nhiều lệnh khác, không chỉ history.

Ví dụ:
docker ps | grep superset


Lọc danh sách container Docker để xem những dòng có chứa superset.
ps aux | grep python


Tìm các dòng tiến trình có chứa python.
cat app.log | grep ERROR


Tìm dòng có chứa ERROR trong log. Cách viết ngắn gọn, thường được ưu tiên hơn, là:
grep 'ERROR' app.log


Mẹo quan trọng: Khi làm việc trên Ubuntu, nếu bạn biết một từ khóa nhưng không nhớ lệnh, file hoặc vị trí cần tìm, hãy nghĩ đến grep. Nó là công cụ lọc văn bản rất hữu ích khi làm việc với Git, Docker, log và mã nguồn.
# id và namei — tìm nguyên nhân Permission denied
Một lỗi khá phổ biến: file có vẻ đúng quyền nhưng Python vẫn không đọc được.

Ví dụ:
PermissionError: [Errno 13] Permission denied: '/opt/app/data/input.json'


Thay vì lập tức dùng sudo, hãy kiểm tra từng lớp quyền.

Bước 1 — kiểm tra user và group hiện tại
id


Output minh họa:
uid=1000(thang) gid=1000(thang) groups=1000(thang),27(sudo),1001(developers)


Bạn đang chạy bằng user thang, thuộc các group thang, sudo, developers.

Bước 2 — kiểm tra quyền trên toàn bộ đường dẫn
namei -l /opt/app/data/input.json


Output minh họa:
f: /opt/app/data/input.json
drwxr-xr-x root root    /
drwxr-xr-x root root    opt
drwxr-x--- root app     app
drwxr-x--- app  app     data
-rw-r----- app  app     input.json


namei -l cho biết quyền và chủ sở hữu của từng thành phần trên đường dẫn.

Điều quan trọng: để truy cập file, user cần có quyền x (traverse) trên các thư mục cha. Có quyền đọc file chưa chắc đã đủ nếu không đi qua được thư mục cha.

Khi nào dùng?
- Python không đọc được file cấu hình.
- Ứng dụng chạy bằng systemd không truy cập được thư mục.
- File thuộc user root nhưng ứng dụng chạy bằng user thông thường.

chmod — cấp quyền đúng mức
Linux biểu diễn quyền bằng ba nhóm:
- u: chủ sở hữu (user).
- g: nhóm (group).
- o: những người dùng khác (others).
Ba quyền cơ bản:
- r = đọc = 4.
- w = ghi = 2.
- x = thực thi hoặc truy cập thư mục = 1.
Ví dụ:
chmod 640 config.ini


Kết quả quyền tương ứng:
-rw-r-----


Nhóm	Quyền	Giá trị
Chủ sở hữu	Đọc, ghi	6
Group	Đọc	4
Others	Không có quyền	0

Ví dụ khác:
chmod u+x deploy.sh


Thêm quyền thực thi cho chủ sở hữu của file deploy.sh.

Mẹo: Tránh sử dụng chmod -R 777 để sửa lỗi quyền. Nó cấp quyền đọc, ghi và thực thi cho tất cả người dùng trên mọi file/thư mục được áp dụng, có thể gây rủi ro bảo mật.
Lệnh 11: chown — thay đổi chủ sở hữu
Ví dụ:
sudo chown app:app /opt/app/data/input.json


File được chuyển sang user app và group app.

Thay đổi đệ quy cả thư mục:
sudo chown -R app:app /opt/app/data


Cẩn thận với -R: hãy chắc chắn bạn đang chỉ định đúng thư mục, vì toàn bộ file và thư mục con có thể bị đổi chủ sở hữu.

Một nguyên tắc hữu ích: nếu ứng dụng cần sở hữu dữ liệu, hãy cân nhắc cấp quyền cho đúng user/group chạy ứng dụng, thay vì chạy ứng dụng bằng root.

5. Log và điều tra lỗi dịch vụ
Lệnh 12: journalctl — đọc log hệ thống và dịch vụ
Khi bạn chạy ứng dụng dưới dạng systemd service, log thường có thể được truy vấn bằng journalctl. Công cụ này hỗ trợ lọc theo service, thời gian và nhiều trường dữ liệu. 
Ubuntu Manpages+1


Giả sử service của bạn tên my-api.service.

Xem log của service:
journalctl -u my-api.service


Chỉ xem 100 dòng cuối:
journalctl -u my-api.service -n 100


Theo dõi log trực tiếp:
journalctl -u my-api.service -f


Tùy chọn -f hoạt động tương tự tail -f, rất tiện khi bạn restart ứng dụng và muốn quan sát lỗi mới xuất hiện.

Xem log trong 30 phút gần nhất:
journalctl -u my-api.service --since "30 minutes ago"


Chỉ xem log từ lần khởi động gần nhất:
journalctl -u my-api.service -b


Ví dụ output:
Oct 29 16:10:12 server my-api[2451]: Starting application
Oct 29 16:10:13 server my-api[2451]: Database connection failed
Oct 29 16:10:13 server systemd[1]: my-api.service: Failed with result 'exit-code'.


Bạn biết ứng dụng không khởi động thành công và có lỗi kết nối database.
Lệnh 13: grep — lọc log theo nhiều điều kiện
Giả sử file log có hàng triệu dòng nhưng bạn chỉ muốn tìm lỗi.
grep -in "error" app.log


- -i: không phân biệt chữ hoa/chữ thường.
- -n: hiển thị số dòng.
Tìm nhiều loại lỗi:
grep -Ein "error|exception|traceback|failed" app.log


Dấu | trong Regex có nghĩa là hoặc. Lệnh này tìm dòng chứa bất kỳ mẫu nào trong bốn mẫu trên.

Chỉ tìm lỗi trong 200 dòng cuối:
tail -n 200 app.log | grep -Ein "error|exception|failed"


Đây là một ví dụ về pipeline: tail đưa kết quả ra đầu ra chuẩn, rồi grep nhận dữ liệu đó để lọc.

6. Những lệnh nâng cao giúp xử lý dữ liệu ngay trên terminal
Lệnh 14: find — tìm file theo nhiều tiêu chí
find không chỉ tìm file theo tên; nó còn lọc theo loại, thời gian sửa đổi, dung lượng và thực hiện hành động trên các kết quả. 
Linux manual page


Ví dụ 1 — tìm tất cả file JSON trong thư mục hiện tại và các thư mục con:
find . -type f -name "*.json"


Ví dụ 2 — tìm file log sửa đổi trong 24 giờ qua:
find /var/log -type f -mmin -1440


Ví dụ 3 — tìm file lớn hơn 500 MB:
find /home -type f -size +500M


Ví dụ 4 — tìm file JSON rồi chạy một lệnh cho từng file:
find data -type f -name "*.json" \
  -exec wc -l {} +


Ở đây, {} được thay bằng các file tìm được; dấu + cho phép gom nhiều file vào một lần gọi wc.

Lưu ý: wc -l đếm số dòng, không phải số object JSON. Với JSON được format trên nhiều dòng hoặc JSONL, ý nghĩa kết quả sẽ khác nhau.
Lệnh 15: awk — thống kê dữ liệu dạng cột
awk cực kỳ hữu ích khi bạn cần trích xuất cột, lọc và thống kê mà không muốn viết Python script riêng.

Giả sử file access.log có dữ liệu:
200 GET /health 12
500 POST /login 45
200 GET /items 20
500 GET /items 50


Các cột lần lượt là status code, method, path và thời gian phản hồi.

Đếm số dòng theo status code:
awk '{count[$1]++} END {for (code in count) print code, count[code]}' access.log


Output:
200 2
500 2


Giải thích:
- $1: cột thứ nhất.
- $2: cột thứ hai.
- count[$1]++: tăng bộ đếm tương ứng với status code.
- END: thực hiện phần thống kê sau khi đọc hết file.
Tính thời gian phản hồi trung bình:
awk '{sum += $4; n++} END {if (n) printf "Average: %.2f ms\n", sum/n}' access.log


Output:
Average: 31.75 ms


Đây là ví dụ dữ liệu giả lập có định dạng đơn giản. Log thực tế có thể cần điều chỉnh cách phân tách cột.
Lệnh 16: xargs — biến kết quả của một lệnh thành đối số của lệnh khác
xargs đọc dữ liệu từ standard input và sử dụng dữ liệu đó làm đối số để chạy một lệnh. 
Linux manual page


Ví dụ:
printf 'one\ntwo\nthree\n' | xargs echo


Output:
one two three


Ứng dụng thực tế: tìm các file Python rồi kiểm tra file nào có chuỗi TODO.
find . -type f -name "*.py" -print0 |
  xargs -0 grep -nH "TODO"


- -print0: phân tách tên file bằng ký tự NUL.
- xargs -0: đọc đúng định dạng đó, tránh lỗi với tên file chứa dấu cách hoặc ký tự xuống dòng.
- grep -nH: in số dòng và tên file.
Một lưu ý quan trọng: Khi chạy các lệnh có tác động như xóa file, hãy kiểm tra danh sách kết quả trước. Không nên ghép find và xargs rm một cách tùy tiện.

7. Một số lệnh nhỏ nhưng cực kỳ hữu ích
Đây là những lệnh mình khuyên bạn nên học tiếp vì chúng giúp tiết kiệm thời gian mỗi ngày.
watch — tự động chạy lại một lệnh

watch -n 2 'ss -lntp'


Cứ mỗi 2 giây, hiển thị lại các port đang lắng nghe. Hữu ích khi đợi ứng dụng khởi động. Nhấn Ctrl+C để thoát.


timeout — giới hạn thời gian chạy

timeout 10s curl -v http://127.0.0.1:8000/health


Dừng lệnh sau khoảng 10 giây nếu nó vẫn chưa kết thúc. Hữu ích với script hoặc kết nối có nguy cơ bị treo. Lệnh con có thể cần xử lý signal đúng cách.


tee — vừa xem output vừa lưu ra file

python -m myapp 2>&1 | tee run.log


Hiển thị output trong terminal đồng thời ghi vào run.log. 2>&1 chuyển cả stderr vào stdout để tee nhận được cả lỗi. Mặc định, file log cũ sẽ bị ghi đè.


diff — so sánh hai file

diff -u config.old config.new


Hiển thị các dòng khác nhau giữa hai file, rất tiện khi so sánh cấu hình trước và sau khi sửa.


man — đọc tài liệu ngay trong terminal

man ss
man journalctl
man find


Nhấn /keyword để tìm trong tài liệu, n để đến kết quả tiếp theo và q để thoát.


8. Thực hành một tình huống thực tế
Giả sử bạn triển khai FastAPI trên Ubuntu và gặp lỗi không truy cập được API ở port 8000. Hãy xử lý theo thứ tự sau.
Checklist chẩn đoán API
[ ] 1. Xác nhận port có đang lắng nghe không.

ss -lntp 'sport = :8000'


[ ] 2. Xem Uvicorn có đang chạy không.

pgrep -af uvicorn


[ ] 3. Kiểm tra HTTP từ chính máy chạy API.

curl -v --max-time 5 http://127.0.0.1:8000/health


[ ] 4. Kiểm tra địa chỉ IP và cấu hình routing.

ip -br addr && ip route


[ ] 5. Nếu chạy bằng systemd, đọc 100 dòng log gần nhất.

journalctl -u my-api.service -n 100 --no-pager


[ ] 6. Nếu API phụ thuộc PostgreSQL trên máy khác, kiểm tra TCP tới database.

nc -vz 192.168.9.56 5432


0/6 bước đã kiểm tra

Các lệnh trên giúp bạn phân biệt một số nguyên nhân khác nhau:
- Không có port: ứng dụng chưa khởi động hoặc đang listen ở port khác.
- Có port nhưng curl lỗi: kiểm tra route, ứng dụng và log.
- Local truy cập được nhưng máy khác không truy cập được: kiểm tra địa chỉ bind, firewall, routing và cấu hình mạng.
- API chạy nhưng database không kết nối được: kiểm tra địa chỉ database, port, firewall và cấu hình PostgreSQL.
Không nên kết luận rằng firewall có lỗi chỉ vì kết nối thất bại; hãy dùng kết quả của từng bước để thu hẹp nguyên nhân.
9. Lộ trình học mình đề xuất
Với công việc lập trình Python trên Ubuntu, mình sẽ ưu tiên theo thứ tự:
Giai đoạn	Nhóm kiến thức	Lệnh cần thành thạo
1	Debug mạng và port	ss, lsof, curl, nc, ip
2	Process và tài nguyên	ps, pgrep, kill, free, df, du
3	Quyền truy cập	id, namei, chmod, chown, getfacl
4	Log và tìm kiếm	journalctl, grep, find, awk, tail
5	Kết hợp lệnh	xargs, tee, watch, timeout, sort, uniq
6	Quản trị hệ thống sâu hơn	systemctl, sysctl, lsof, strace, tcpdump

Giai đoạn 6 sẽ đi sâu hơn vào cách process hoạt động, system call, kernel parameters và phân tích lưu lượng mạng. Với strace và tcpdump, bạn có thể điều tra các lỗi khó mà log ứng dụng thông thường không giải thích được.

Một nguyên tắc rất đáng nhớ: đừng học Linux chỉ bằng cách ghi nhớ cú pháp. Hãy học cách đặt câu hỏi cho hệ thống: process nào đang chạy, port nào đang lắng nghe, user nào đang thực thi, tài nguyên nào đang cạn, và log nào chứng minh nguyên nhân? Khi làm được điều đó, bạn sẽ xử lý sự cố nhanh hơn rất nhiều.