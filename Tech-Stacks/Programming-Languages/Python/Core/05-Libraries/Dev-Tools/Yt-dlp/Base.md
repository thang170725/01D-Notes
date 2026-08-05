- [Introduction](#introduction)
- [YoutubeDL() (Tạo đối tượng cấu hình)](#youtubedl-tạo-đối-tượng-cấu-hình)
  - [.download() (Tải video/audio)](#download-tải-videoaudio)
---
# Introduction
# YoutubeDL() (Tạo đối tượng cấu hình)
**Syn**
```bash
ydl = YoutubeDL(options)

- Input:
    options: Là một dictionaries gồm:
        - "format":  
            + "best": tải file tốt nhất có thê
            + "worst": file thấp nhất
            + "bestaudio": chỉ lấy audio tốt nhất
            + "bestvideo+bestaudio": video tốt nhất + audio tốt nhất. sau đó ffmpeg sẽ ghép lại  
        - "outmpl": cấu hình nơi lưu file
        - "noplaylist": chỉ tải video hiện tại không tải cả playlist
```
## .download() (Tải video/audio)
**Syn**
```bash
ydl.download([url])
```
**Ex**
```python
with YoutubeDL() as ydl:
    ydl.download([
        "https://youtube.com/watch?v=abc"
    ])

# Downloading...100%Saved: video.mp4
```
1. extract_info()
Dùng để làm gì
Lấy thông tin video mà không cần tải.
Cú pháp
info = ydl.extract_info(url, download=False)
Ví dụ
with YoutubeDL() as ydl:    info = ydl.extract_info(url, download=False)print(info["title"])
Kết quả giả định
Python Tutorial

1. prepare_filename()
Dùng để làm gì
Sinh tên file theo template.
Ví dụ
filename = ydl.prepare_filename(info)print(filename)
Kết quả giả định
Python Tutorial.mp4

1. sanitize_info()
Dùng để làm gì
Chuyển metadata sang dạng an toàn để lưu JSON.
Ví dụ
clean = ydl.sanitize_info(info)

Các option quan trọng
6. Chọn chất lượng
Video tốt nhất
{    "format": "best"}
Ví dụ:
YoutubeDL({    "format": "best"})

7. Chọn audio tốt nhất
{    "format": "bestaudio"}
Ví dụ:
YoutubeDL({    "format": "bestaudio"})

8. Chuyển sang mp3
Cú pháp
{    "format": "bestaudio",    "postprocessors": [...]}
Ví dụ
opts = {    "format": "bestaudio",    "postprocessors": [{        "key": "FFmpegExtractAudio",        "preferredcodec": "mp3",        "preferredquality": "192",    }],}
Kết quả giả định
song.mp3

Cần cài FFmpeg.


9. Đặt tên file
Cú pháp
{    "outtmpl": "%(title)s.%(ext)s"}
Ví dụ
YoutubeDL({    "outtmpl": "%(uploader)s - %(title)s.%(ext)s"})
Kết quả giả định
CodeBasics - Python Tutorial.mp4

10. Tải playlist
ydl.download([    "https://youtube.com/playlist?list=..."])
Kết quả giả định
Video 1.mp4Video 2.mp4Video 3.mp4

11. Chỉ tải một vài video trong playlist
Ví dụ
YoutubeDL({    "playlist_items": "1,3,5"})
Kết quả giả định
Downloaded videos:135

12. Lấy danh sách format
Ví dụ
info = ydl.extract_info(url, download=False)for f in info["formats"]:    print(        f["format_id"],        f.get("ext"),        f.get("height")    )
Kết quả giả định
18 mp4 36022 mp4 720137 mp4 1080251 webm None

13. Tải subtitle
YoutubeDL({    "writesubtitles": True})
Kết quả giả định
video.en.vtt

14. Tải subtitle tự động
YoutubeDL({    "writeautomaticsub": True})
Kết quả giả định
auto.en.vtt

15. Chọn ngôn ngữ subtitle
YoutubeDL({    "subtitleslangs": ["en", "vi"]})
Kết quả giả định
Downloaded:en subtitlevi subtitle

16. Tải thumbnail
YoutubeDL({    "writethumbnail": True})
Kết quả giả định
thumbnail.webp

17. Theo dõi tiến trình tải
Ví dụ
def hook(d):    print(d["status"])YoutubeDL({    "progress_hooks": [hook]})
Kết quả giả định
downloadingfinished

18. Bỏ qua lỗi để tải tiếp
YoutubeDL({    "ignoreerrors": True})
Kết quả giả định
Video 2 failedContinue downloading...

19. Không tải, chỉ mô phỏng
YoutubeDL({    "simulate": True})
Kết quả giả định
Would download:Python Tutorial.mp4

20. Ghi log chi tiết
YoutubeDL({    "verbose": True})
Kết quả giả định
[debug] Extracting info...[debug] Downloading webpage...

Một số khóa metadata hay dùng
Sau khi:
info = ydl.extract_info(url, download=False)
bạn thường dùng:
info["title"]        # tiêu đềinfo["uploader"]     # kênh đănginfo["duration"]     # số giâyinfo["view_count"]   # lượt xeminfo["upload_date"]  # ngày đănginfo["thumbnail"]    # URL thumbnailinfo["description"]  # mô tảinfo["formats"]      # danh sách formatinfo["webpage_url"]  # URL video
Ví dụ kết quả giả định:
{    "title": "Learn Python",    "uploader": "Code Channel",    "duration": 540,    "view_count": 125000}

5 thứ quan trọng nhất cần nhớ
Nếu mới học yt-dlp, chỉ cần nhớ:
YoutubeDL(...)ydl.download(...)ydl.extract_info(...)formatouttmpl
Kết hợp lại, bạn đã làm được gần như mọi tác vụ phổ biến:


Tải video.


Tải MP3.


Lấy metadata.


Tải playlist.


Tải subtitle/thumbnail.


Chọn chất lượng tải.

