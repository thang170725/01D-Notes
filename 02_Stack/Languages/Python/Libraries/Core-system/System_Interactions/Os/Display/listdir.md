# .listdir()
```bash
Liệt kê tên file/thư mục trong thư mục.
```
**Ex1**
```python
import os
print(os.listdir('.')) # ['test.py', 'output.txt', 'images', '.venv', 'input.txt']
```
**Ex2: liệt kê tất cả các file .txt trong thư mục**
```python
import os
for filename in os.listdir("."):
    if filename.endswith(".txt"):
        print(filename)
```