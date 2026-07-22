- [Logging Introduction](#logging-introduction)
- [.getLogger() (hàm để lấy hoặc tạo một đối tượng Logger)](#getlogger-hàm-để-lấy-hoặc-tạo-một-đối-tượng-logger)
  - [.info()](#info)
  - [.debug()](#debug)
- [basicConfig()](#basicconfig)
- [.getLogger()](#getlogger)
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
## .info()
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
# .getLogger()