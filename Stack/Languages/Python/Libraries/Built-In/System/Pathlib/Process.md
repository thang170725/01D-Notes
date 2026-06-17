- [Path (Tạo đối tượng)](#path-tạo-đối-tượng)
  - [.mkdir (Tạo thư mục)](#mkdir-tạo-thư-mục)
  - [.cwd() (thư mục làm việc hiện tại)](#cwd-thư-mục-làm-việc-hiện-tại)
---
# Path (Tạo đối tượng)
## .mkdir (Tạo thư mục)
**Syn**
```bash
folder.mkdir()

- exist_ok=True:
    + Nếu thư mục chưa có → tạo mới.
    + Nếu đã có → bỏ qua, không báo lỗi
- parents=True: tự động tạo các thư mục cha nếu chưa có
```
## .cwd() (thư mục làm việc hiện tại)
**Syn**
```bash

- Output: <class 'pathlib.PosixPath'>
```
**Ex**
```python
from pathlib import Path

current_dir = Path.cwd()

print(current_dir)
/home/thang/project
```