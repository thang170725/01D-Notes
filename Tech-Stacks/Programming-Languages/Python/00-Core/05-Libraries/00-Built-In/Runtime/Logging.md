- [Logging Introduction (dùng để ghi lại thông tin trong quá trình chương trình chạy)](#logging-introduction-dùng-để-ghi-lại-thông-tin-trong-quá-trình-chương-trình-chạy)
  - [stdout (standard output)](#stdout-standard-output)
- [basicConfig() (để cấu hình logging)](#basicconfig-để-cấu-hình-logging)
- [.getLogger() (hàm để lấy hoặc tạo một đối tượng Logger)](#getlogger-hàm-để-lấy-hoặc-tạo-một-đối-tượng-logger)
  - [.info()](#info)
  - [.debug()](#debug)
  - [.exception()](#exception)
  - [setLevel() (dùng để đặt mức log tối thiểu mà Logger hoặc Handler sẽ xử lý)](#setlevel-dùng-để-đặt-mức-log-tối-thiểu-mà-logger-hoặc-handler-sẽ-xử-lý)
  - [.addHandler() (dùng để gắn thêm một Handler vào Logger)](#addhandler-dùng-để-gắn-thêm-một-handler-vào-logger)
- [Formatter()](#formatter)
- [StreamHandler() (dùng để ghi log ra một luồng (stream))](#streamhandler-dùng-để-ghi-log-ra-một-luồng-stream)
  - [FileHandler](#filehandler)
- [Hiển thị trên màn hình](#hiển-thị-trên-màn-hình)
- [Ghi vào file](#ghi-vào-file)
---
# Logging Introduction (dùng để ghi lại thông tin trong quá trình chương trình chạy)
```bash
logging là thư viện built-in của Python, nên bạn không cần cài đặt.
    Chỉ cần: import logging là có thể sử dụng.

logging dùng để làm gì?
    Ví dụ:
        - Chương trình chạy đến đâu
        - Có lỗi gì xảy ra
        - Hàm nào đang được gọi
        - Dữ liệu đầu vào là gì
        - Mất bao lâu để xử lý
```
## stdout (standard output)
```bash
là luồng xuất chuẩn của chương trình. Thông thường, nó được hiển thị trên cửa sổ Terminal/Command Prompt.

Ví dụ: print("Xin chào")
    Thực chất, print() ghi dữ liệu ra stdout.
```
**So sánh stdout và stderr**
```bash
Luồng	Mục đích	                Mặc định hiển thị ở đâu
stdout	Xuất kết quả bình thường	Terminal/Command Prompt
stderr	Xuất thông báo lỗi	        Terminal/Command Prompt
# Cả hai đều thường xuất hiện trên màn hình, nhưng chúng là hai luồng khác nhau.
```
**Ex**
```python
import sys

print("Đây là stdout")

sys.stderr.write("Đây là stderr\n")

# Đây là stdout
# Đây là stderr

# Nhìn thì giống nhau, nhưng:
# print() → ghi vào stdout.
# sys.stderr.write() → ghi vào stderr.
```
# basicConfig() (để cấu hình logging)
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
## .exception()
## setLevel() (dùng để đặt mức log tối thiểu mà Logger hoặc Handler sẽ xử lý)
```bash
Các mức log từ thấp đến cao:
    - logging.DEBUG      # 10
    - logging.INFO       # 20
    - logging.WARNING    # 30
    - logging.ERROR      # 40
    - logging.CRITICAL   # 50
```
**Ex1: setLevel() cho Logger**
```python
import logging

logger = logging.getLogger("demo")
logger.setLevel(logging.WARNING)

console = logging.StreamHandler()
logger.addHandler(console)

logger.debug("Đây là DEBUG")
logger.info("Đây là INFO")
logger.warning("Đây là WARNING")
logger.error("Đây là ERROR")

Kết quả:

Đây là WARNING
Đây là ERROR

Vì logger chỉ nhận các log có mức WARNING trở lên.

Ví dụ 2: setLevel(logging.DEBUG)
import logging

logger = logging.getLogger("demo")
logger.setLevel(logging.DEBUG)

console = logging.StreamHandler()
logger.addHandler(console)

logger.debug("DEBUG")
logger.info("INFO")
logger.warning("WARNING")
logger.error("ERROR")

Kết quả:

DEBUG
INFO
WARNING
ERROR

Do mức thấp nhất là DEBUG, nên tất cả đều được in.

Ví dụ 3: setLevel() cho Handler

Logger và Handler có thể có mức khác nhau.

import logging

logger = logging.getLogger("demo")
logger.setLevel(logging.DEBUG)

console = logging.StreamHandler()
console.setLevel(logging.ERROR)

logger.addHandler(console)

logger.debug("DEBUG")
logger.info("INFO")
logger.warning("WARNING")
logger.error("ERROR")

Kết quả:

ERROR

Giải thích:

Logger nhận từ DEBUG trở lên.
Nhưng Handler chỉ xuất từ ERROR trở lên.
Vì vậy chỉ có ERROR được hiển thị.
Ví dụ 4: Dùng basicConfig()
import logging

logging.basicConfig(level=logging.INFO)

logging.debug("DEBUG")
logging.info("INFO")
logging.warning("WARNING")
logging.error("ERROR")

Kết quả:

INFO:root:INFO
WARNING:root:WARNING
ERROR:root:ERROR
Tóm tắt
setLevel()	Log được hiển thị
logging.DEBUG	DEBUG, INFO, WARNING, ERROR, CRITICAL
logging.INFO	INFO, WARNING, ERROR, CRITICAL
logging.WARNING	WARNING, ERROR, CRITICAL
logging.ERROR	ERROR, CRITICAL
logging.CRITICAL	CRITICAL

Lưu ý: setLevel() chỉ đặt ngưỡng tối thiểu. Ví dụ setLevel(logging.INFO) không có nghĩa là chỉ in INFO, mà sẽ in tất cả các mức từ INFO trở lên (INFO, WARNING, ERROR, CRITICAL).
## .addHandler()
# .Formatter()
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
## .addHandler() (dùng để gắn thêm một Handler vào Logger)
```bash
Có thể hiểu đơn giản:
    - Logger = người tạo ra log.
    - Handler = nơi nhận log (màn hình, file,...).
    - addHandler() = nối Logger với Handler.
```
**Ex1: Hiển thị log trên màn hình**
```python
import logging

# Tạo Logger
logger = logging.getLogger("Demo")
logger.setLevel(logging.DEBUG)

# Tạo Handler
console = logging.StreamHandler()

# Gắn Handler vào Logger
logger.addHandler(console)

# Gửi log
logger.info("Xin chào")
logger.error("Có lỗi")

# Xin chào
# Có lỗi
# Nếu không có dòng: logger.addHandler(console) thì logger.info() và logger.error() sẽ không được hiển thị (vì Logger chưa biết phải gửi log đi đâu).
```
**Ex2: Ghi log vào file**
import logging

logger = logging.getLogger("Demo")
logger.setLevel(logging.INFO)

file = logging.FileHandler("log.txt")

logger.addHandler(file)

logger.info("Đăng nhập thành công")

Sau khi chạy, file log.txt sẽ có:

Đăng nhập thành công
Ví dụ 3: Một Logger có nhiều Handler

Một Logger có thể gửi log đến nhiều nơi cùng lúc.

import logging

logger = logging.getLogger("Demo")
logger.setLevel(logging.INFO)

console = logging.StreamHandler()
file = logging.FileHandler("log.txt")

logger.addHandler(console)
logger.addHandler(file)

logger.info("Xin chào")

Kết quả:

Trên màn hình:

Xin chào

Trong file log.txt:

Xin chào

Chỉ gọi logger.info() một lần, nhưng log được gửi đến 2 Handler nên xuất hiện ở cả màn hình và file.

Hình dung dễ nhớ
          logger.info("Xin chào")
                   |
                 Logger
                   |
        ---------------------
        |                   |
 addHandler()         addHandler()
        |                   |
 StreamHandler       FileHandler
        |                   |
    Màn hình            log.txt

addHandler() giống như cắm thêm một "đầu ra" cho Logger. Mỗi lần Logger tạo log, nó sẽ gửi bản sao của log đến tất cả các Handler đã được thêm bằng addHandler().
# Formatter()
# StreamHandler() (dùng để ghi log ra một luồng (stream))
Trong logging.StreamHandler
import logging

handler = logging.StreamHandler()

Mặc định tương đương:

import logging
import sys

handler = logging.StreamHandler(sys.stderr)

Nghĩa là log sẽ được ghi vào stderr.

Nếu muốn ghi vào stdout:

import logging
import sys

handler = logging.StreamHandler(sys.stdout)
Tại sao phải tách stdout và stderr?

Ví dụ chạy chương trình:

python demo.py > output.txt
stdout sẽ được ghi vào output.txt.
stderr vẫn hiển thị trên màn hình.

Ví dụ:

import sys

print("Kết quả")
sys.stderr.write("Lỗi!\n")

Chạy:

python demo.py > output.txt

Màn hình:

Lỗi!

Nội dung output.txt:

Kết quả

Đó là lý do logging mặc định dùng stderr: log và thông báo lỗi không bị lẫn với kết quả đầu ra (stdout) của chương trình.
**Syn**
```bash
- Output: mặc định là màn hình (console - sys.stderr). Ngoài ra, bạn cũng có thể ghi ra sys.stdout.
```
**Ex1: StreamHandler cơ bản**
```python
import logging

logger = logging.getLogger("Demo")
logger.setLevel(logging.DEBUG)

# Tạo StreamHandler
console = logging.StreamHandler()

logger.addHandler(console)

logger.debug("Đây là DEBUG")
logger.info("Đây là INFO")
logger.warning("Đây là WARNING")

# Đây là DEBUG
# Đây là INFO
# Đây là WARNING
```
**Ví dụ 2: StreamHandler kết hợp Formatter**
```python
import logging

logger = logging.getLogger("Demo")
logger.setLevel(logging.DEBUG)

console = logging.StreamHandler()

formatter = logging.Formatter(
    "%(asctime)s - %(levelname)s - %(message)s"
)

console.setFormatter(formatter)

logger.addHandler(console)

logger.info("Chương trình bắt đầu")
logger.error("Có lỗi xảy ra")

# 2026-07-30 08:20:15,123 - INFO - Chương trình bắt đầu
# 2026-07-30 08:20:15,124 - ERROR - Có lỗi xảy ra
```
**Ex3: StreamHandler với setLevel()**
```python
import logging

logger = logging.getLogger("Demo")
logger.setLevel(logging.DEBUG)

console = logging.StreamHandler()
console.setLevel(logging.ERROR)

logger.addHandler(console)

logger.debug("DEBUG")
logger.info("INFO")
logger.warning("WARNING")
logger.error("ERROR")

# ERROR - Vì StreamHandler chỉ nhận log từ ERROR trở lên.
```
**Ex4: Ghi ra stdout**
```bash
Mặc định StreamHandler() ghi ra sys.stderr. Nếu muốn ghi ra stdout:
```
```python
import logging
import sys

logger = logging.getLogger("Demo")
logger.setLevel(logging.INFO)

console = logging.StreamHandler(sys.stdout)

logger.addHandler(console)

logger.info("Xin chào!")

# Xin chào!
```
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
Ví dụ 5: Dùng nhiều Handler

Có thể vừa ghi ra màn hình, vừa ghi ra file:

import logging

logger = logging.getLogger("Demo")
logger.setLevel(logging.DEBUG)

# Hiển thị trên màn hình
console = logging.StreamHandler()

# Ghi vào file
file = logging.FileHandler("log.txt")

logger.addHandler(console)
logger.addHandler(file)

logger.info("Đăng nhập thành công")
logger.error("Không tìm thấy dữ liệu")

Kết quả:

Console hiển thị:
Đăng nhập thành công
Không tìm thấy dữ liệu
File log.txt cũng chứa:
Đăng nhập thành công
Không tìm thấy dữ liệu
Tóm tắt
logging.StreamHandler() → ghi log ra console (stderr mặc định).
logging.StreamHandler(sys.stdout) → ghi log ra stdout.
Có thể dùng:
setLevel() để lọc mức log.
setFormatter() để định dạng log.
addHandler() để gắn StreamHandler vào Logger.