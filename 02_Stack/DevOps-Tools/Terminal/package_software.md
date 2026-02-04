- [Install \& run .deb](#install--run-deb)
- [Cài GIMP (remove background img)](#cài-gimp-remove-background-img)
- [Tải video](#tải-video)
- [Cài bộ gõ tiếng việt (linux)](#cài-bộ-gõ-tiếng-việt-linux)
- [Gỡ, xóa phần mềm, …](#gỡ-xóa-phần-mềm-)
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
```bash
1. dpkg -l | grep chrome: Tìm phần mềm đã cài.
2. sudo apt remove google-chrome-stable: Gỡ phần mềm. | sudo apt purge google-chrome-stable: Nếu muốn gỡ sạch hơn.
3. sudo apt autoremove: Dọn lại hệ thống (xóa gói đã cài nhưng không cần nữa).
4. sudo apt clean: Xóa cache tải về của apt. | sudo apt autoclean: Nếu muốn dọn triệt để hơn (chỉ giữ lại vài file).
```