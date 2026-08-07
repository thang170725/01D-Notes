Đúng vậy.

subprocess là thư viện built-in (thư viện chuẩn) của Python, nên không cần cài đặt bằng pip.

Chỉ cần:

import subprocess

là dùng được.

subprocess dùng để làm gì?

Nó dùng để tạo và quản lý một tiến trình (process) khác từ Python.

Hiểu đơn giản là:

Python có thể gọi một chương trình khác để chạy.

Ví dụ

Python

↓

chạy

Git
FFmpeg
Docker
Java
NodeJS
PowerShell
CMD
Python khác
Ví dụ 1: Chạy lệnh dir

Windows

import subprocess

subprocess.run(["cmd", "/c", "dir"])

Kết quả giống như bạn gõ

dir
Ví dụ 2: Chạy Python khác
subprocess.run([
    "python",
    "train.py"
])

Giống như

python train.py
Ví dụ 3: Gọi Git
subprocess.run([
    "git",
    "status"
])

Tương đương

git status
Ví dụ 4: Gọi FFmpeg
subprocess.run([
    "ffmpeg",
    "-i",
    "video.mp4",
    "video.avi"
])

Python không tự convert video.

Nó chỉ bảo FFmpeg chạy.

Có thể lấy kết quả trả về
import subprocess

result = subprocess.run(
    ["git", "status"],
    capture_output=True,
    text=True
)

print(result.stdout)

Kết quả

On branch main

nothing to commit
Kiểm tra lỗi
result = subprocess.run(
    ["git", "status"],
    capture_output=True,
    text=True
)

print(result.returncode)
0

0

↓

Thành công

Nếu

1

↓

Có lỗi.

subprocess.Popen

Nếu muốn chạy lâu

Ví dụ train YOLO

process = subprocess.Popen([
    "python",
    "train.py"
])

Python sẽ không đợi.

Nó chạy tiếp.

Sau đó

process.wait()

đợi train xong.

subprocess.run

Ngược lại

subprocess.run([
    "python",
    "train.py"
])

Python sẽ

↓

Đợi

↓

Train xong

↓

Mới chạy dòng tiếp theo.

So sánh với os.system

Ngày xưa hay dùng

import os

os.system("git status")

Hiện nay khuyến nghị dùng

subprocess.run(["git", "status"])

Vì:

An toàn hơn (không phải tự ghép chuỗi lệnh).
Dễ lấy stdout, stderr, mã trả về.
Hoạt động ổn định trên nhiều hệ điều hành.
Trong các project AI

subprocess được dùng rất nhiều để:

Gọi script train:
subprocess.run(["python", "train.py"])
Gọi script predict:
subprocess.run(["python", "predict.py"])
Xuất mô hình:
subprocess.run(["python", "export.py"])
Gọi Git:
subprocess.run(["git", "pull"])
Gọi Docker:
subprocess.run(["docker", "build", "."])
Gọi FFmpeg xử lý video.
Tóm tắt
✅ subprocess là thư viện chuẩn (built-in/standard library) của Python.
✅ Dùng để chạy và quản lý các chương trình hoặc lệnh bên ngoài từ Python.
✅ subprocess.run() phù hợp khi muốn chạy xong rồi mới tiếp tục.
✅ subprocess.Popen() phù hợp khi muốn tiến trình chạy song song hoặc cần tương tác với tiến trình đó.