- [.NamedTemporaryFile (Tạo một file tạm có tên thật trên ổ đĩa)](#namedtemporaryfile-tạo-một-file-tạm-có-tên-thật-trên-ổ-đĩa)
  - [.name (đường dẫn file)](#name-đường-dẫn-file)
  - [.read() (đọc file tạm)](#read-đọc-file-tạm)
  - [.write() (ghi vào file)](#write-ghi-vào-file)
  - [.close() (đóng file)](#close-đóng-file)
---
# .NamedTemporaryFile (Tạo một file tạm có tên thật trên ổ đĩa)
**Syn**
```bash
tempfile.NamedTemporaryFile(
    mode='w+b',
    buffering=-1,
    encoding=None,
    newline=None,
    suffix=None,
    prefix=None,
    dir=None,
    delete=True
)

- Input:
    + mode      : chế độ mở file
    + suffix	: đuôi file
    + prefix	: tiền tố tên file
    + dir	    : thư mục lưu
    + delete	: tự xóa khi đóng. 
        - True  : mặc định là True (khi thoát khỏi with sẽ xóa file)
        - False : Không xóa
```
**Ex: Tạo file tạm**
```python
import tempfile

with tempfile.NamedTemporaryFile(
        suffix=".pdf",
        delete=False
) as f:

    print(f.name)
```
## .name (đường dẫn file)
**Ex**
```python
import tempfile

with tempfile.NamedTemporaryFile() as f:
    print(f.name) # /tmp/tmp7h8x2abc
```
## .read() (đọc file tạm)
**Ex: Ghi và đọc file tạm**
```python
import tempfile

with tempfile.NamedTemporaryFile(mode="w+") as f:
    f.write("Hello")
    f.seek(0)

    print(f.read())
```
## .write() (ghi vào file)
## .close() (đóng file)