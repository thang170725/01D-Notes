- [Install \& run .deb](#install--run-deb)
- [Cài GIMP (remove background img)](#cài-gimp-remove-background-img)
- [Installation LibreOffice](#installation-libreoffice)
- [Tải video](#tải-video)
- [Cài bộ gõ tiếng việt (linux)](#cài-bộ-gõ-tiếng-việt-linux)
- [Gỡ, xóa phần mềm, …](#gỡ-xóa-phần-mềm-)
- [Cách mở khóa Office 365](#cách-mở-khóa-office-365)
---
# Install & run .deb
```bash
1. sudo apt update
2. sudo apt install ./google.deb
```
# Cài GIMP (remove background img)
```bash
sudo apt install gimp     # Ubuntu / Debian
sudo pacman -S gimp       # Arch
sudo dnf install gimp     # Fedora
```
# Installation LibreOffice
```bash
1. sudo apt update
2. sudo apt install libreoffice
```
# Tải video
**Step**
```bash
1. sudo apt update
2. sudo apt install yt-dlp -y
3.
yt-dlp "https://www.youtube.com/watch?v=ABC123"
yt-dlp -f best "https://www.youtube.com/watch?v=ABC123"
yt-dlp -f bestaudio "https://www.youtube.com/watch?v=ABC123" -o "%(title)s.%(ext)s"
yt-dlp -x --audio-format mp3 "https://www.youtube.com/watch?v=ABC123"
yt-dlp -f best "https://www.youtube.com/playlist?list=PLxxxx"
yt-dlp -o "%(title)s.%(ext)s" "https://www.youtube.com/watch?v=ABC123"
python -m yt_dlp "https://www.youtube.com/watch?v=4ar4bwuJwLo"
echo 'alias ytd="python -m yt_dlp --merge-output-format mp4"' >> ~/.bashrc
source ~/.bashrc
4. ytd https://www.youtube.com/shorts/4ar4bwuJwLo
```
**Fix lỗi av1**
```bash
ffmpeg -i dance_korea.mp4 -c:v libx264 -c:a aac output.mp4 # thường xuất hiện trên ubuntu
```
# Cài bộ gõ tiếng việt (linux)
    1. sudo add-apt-repository ppa:bamboo-engine/ibus-bamboo: Thêm PPA chính thức của Bamboo.
    2. sudo apt install software-properties-common: Nếu máy chưa có add-apt-repository thì cài thêm cái này.
    3. dpkg -l | grep bamboo: Kiểm tra xem đã cài bộ cài tiếng việt chưa.
    4. sudo apt update
    5. sudo apt install ibus-bamboo: Cài đặt ibus-bamboo.
    6. ibus restart: Thiết lập để sử dụng.
    7. Sau đó vào settings -> Region & Lanuage -> …
# Gỡ, xóa phần mềm, …
**Ex: Uninstall libreoffice**
```bash
1. Kiểm tra gói đã cài
    + dpkg -l | grep libreoffice    # Tìm phần mềm đã cài.
    + snap list | grep libreoffice
2. Gỡ phần mềm
    + sudo apt remove libreoffice
    + sudo apt purge 'libreoffice*' # Lệnh này sẽ xóa tất cả gói bắt đầu bằng libreoffice
3. Dọn sạch các gói phụ thuộc + file cấu hình
    + sudo apt autoremove --purge
    + sudo apt autoclean
4. Xóa dữ liệu LibreOffice trong thư mục người dùng
    + rm -rf ~/.config/libreoffice
    + rm -rf ~/.cache/libreoffice
    + rm -rf ~/.local/share/libreoffice
```
# Cách mở khóa Office 365
```bash
1. powershell iex (irm https://get.activated.win)
2. nhập số 2
3. nhập số 1
```