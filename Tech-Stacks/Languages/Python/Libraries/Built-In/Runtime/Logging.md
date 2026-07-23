- [Logging Introduction](#logging-introduction)
- [basicConfig()](#basicconfig)
- [.getLogger() (hàm để lấy hoặc tạo một đối tượng Logger)](#getlogger-hàm-để-lấy-hoặc-tạo-một-đối-tượng-logger)
  - [.info()](#info)
  - [.debug()](#debug)
  - [setLevel()](#setlevel)
  - [.addHandler()](#addhandler)
- [Handler (nơi nhận log)](#handler-nơi-nhận-log)
  - [StreamHandler()](#streamhandler)
  - [FileHandler](#filehandler)
---
# Logging Introduction
```bash
logging là thư viện built-in (thư viện chuẩn) của Python, nên bạn không cần cài đặt.
    Chỉ cần: import logging là có thể sử dụng.

logging dùng để làm gì?
    logging dùng để ghi lại thông tin trong quá trình chương trình chạy.

    Ví dụ:
        - Chương trình chạy đến đâu
        - Có lỗi gì xảy ra
        - Hàm nào đang được gọi
        - Dữ liệu đầu vào là gì
        - Mất bao lâu để xử lý
```
# basicConfig()
```bash
Python có một quy tắc:
    Nếu bạn chưa cấu hình logging thì Root Logger chỉ hiển thị các log từ mức WARNING trở lên.
```
**Syn**
```bash
import logging

logging.basicConfig(
    level=logging.DEBUG,
    format="%(levelname)s - %(message)s"
)

- Input:
    + Level:
        - DEBUG	    : Thông tin rất chi tiết, dùng khi debug
        - INFO	    : Thông tin bình thường
        - WARNING	: Cảnh báo
        - ERROR	    : Có lỗi xảy ra
        - CRITICAL	: Lỗi nghiêm trọng
```
**Ex**
```python
import logging

logging.basicConfig(level=logging.INFO)

logging.info("Đang chia...")

print(10 / 2)
# INFO:root:Đang chia...
# 5.0
```
**Ex**
```python
import logging

logging.basicConfig(level=logging.DEBUG)

logging.debug("Đây là debug")
logging.info("Đây là info")
logging.warning("Đây là warning")
logging.error("Đây là error")
logging.critical("Đây là critical")
# DEBUG:root:Đây là debug
# INFO:root:Đây là info
# WARNING:root:Đây là warning
# ERROR:root:Đây là error
# CRITICAL:root:Đây là critical
```
# .getLogger() (hàm để lấy hoặc tạo một đối tượng Logger)
```bash
Logger là gì
    Hãy tưởng tượng bạn là giáo viên. Có một cuốn sổ ghi chép.
        Sổ ghi chép
        ────────────
        09:00 Học sinh A vào lớp
        09:05 Học sinh B vào lớp
        09:10 Kiểm tra bài cũ

    getLogger() nghĩa là "Cho tôi một cuốn sổ ghi chép."
```
**Ex**
```python
import logging

logger = logging.getLogger("demo")
print(logger) # Khi bạn print() một object, Python sẽ gọi hàm __repr__() của object đó.
# <Logger demo (WARNING)>
# Logger → đây là đối tượng Logger
# demo → tên logger
# WARNING → mức log mặc định
```
## .info()
**Ex**
```python
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger("demo")
logger.info("đăng nhập thành công")
# INFO:demo:đăng nhập thành công
```
## .debug()
**Ex**
```python
import logging

logging.basicConfig(level=logging.DEBUG)

logger = logging.getLogger()

logger.debug("Đây là debug")
logger.info("Đây là info")
logger.warning("Đây là warning")
# DEBUG:root:Đây là debug
# INFO:root:Đây là info
# WARNING:root:Đây là warning
```
## setLevel()
## .addHandler()
# Handler (nơi nhận log)
```bash
Ví dụ bạn viết một thông báo.
    Thông báo đó có thể:
        - 📺 Hiện lên màn hình
        - 📄 Ghi vào file
        - 📧 Gửi email
        - 📱 Gửi lên Telegram

    Ai quyết định điều đó?
        👉 Handler.
```
**Ex1: Không dùng Handler**
```bash
message = "Đăng nhập thành công"

print(message) # Thì thông báo chỉ hiện ra màn hình. Đăng nhập thành công

# Nhưng nếu bạn muốn vừa hiện màn hình vừa lưu file thì sao?
# Bạn phải tự viết
with open("log.txt", "a") as f:
    f.write(message + "\n")
# Điều này khá bất tiện.
```
**Ex2: Tự tạo Handler**
```python
# Giả sử bạn muốn mỗi lần log đều có chữ ">>>"

import logging

class MyHandler(logging.Handler):
    def emit(self, record):
        print(">>>", record.getMessage())

logger = logging.getLogger("demo")
logger.setLevel(logging.INFO)
logger.addHandler(MyHandler())

logger.info("Đọc file")
logger.info("Xong")
# >>> Đọc file
# >>> Xong

# Ở đây emit() được gọi tự động mỗi lần logger.info(...) được chạy.
```
## StreamHandler()
**Ex: Logging + Handler**
```python
import logging

logger = logging.getLogger("demo")
logger.setLevel(logging.INFO)

handler = logging.StreamHandler()

logger.addHandler(handler)

logger.info("Hello")
# Hello

# Điều gì xảy ra?
# logger.info("Hello")
# ↓
# Logger tạo log
# ↓
# Handler nhận log
# ↓
# Handler in ra màn hình
```
## FileHandler
**Ex**
```python
import logging

logger = logging.getLogger("demo")
logger.setLevel(logging.INFO)

handler = logging.FileHandler("log.txt")

logger.addHandler(handler)

logger.info("Hello")

# Lần này Terminal (không có gì)
# Nhưng trong file.Hello
```
**Ex2: Hai Handler cùng lúc**
```python
import logging

logger = logging.getLogger("demo")
logger.setLevel(logging.INFO)

screen = logging.StreamHandler()

file = logging.FileHandler("log.txt")

logger.addHandler(screen)
logger.addHandler(file)

logger.info("Xin chào")

# Điều gì xảy ra?
# logger.info()

#         │
#         ▼
#      Logger
#         │
#  ┌──────┴──────┐
#  ▼             ▼
# Screen      File
#  ▼             ▼
# Màn hình    log.txt

# Kết quả
# Terminal: Xin chào
# File: Xin chào
```
