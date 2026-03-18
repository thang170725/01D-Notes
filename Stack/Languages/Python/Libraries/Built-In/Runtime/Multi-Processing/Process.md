- [Create \& Config (tạo \& cấu hình)](#create--config-tạo--cấu-hình)
  - [.Process() \& .start() \&.join()](#process--start-join)
  - [Pool](#pool)
- [Display (cung cấp thông tin)](#display-cung-cấp-thông-tin)
  - [cpu\_count()](#cpu_count)
- [Process (xử lý)](#process-xử-lý)
  - [.map](#map)
  - [.apply()](#apply)
  - [apply\_async()](#apply_async)
  - [.imap()](#imap)
  - [Queue()](#queue)
    - [.put()](#put)
---
# Create & Config (tạo & cấu hình)
## .Process() & .start() &.join()
**Syn**
```bash
from multiprocessing import Process

p = mp.Process(target=func, args=(a, b))
p.start()
p.join()
```
**Ex**
```python
from multiprocessing import Process
import time

def task(name):
    print(f"Start {name}")
    time.sleep(2)
    print(f"End {name}")

if __name__ == "__main__":
    p1 = Process(target=task, args=("A",))
    p2 = Process(target=task, args=("B",))

    p1.start()
    p2.start()

    p1.join()
    p2.join()

    print("Done")

# ✅ Kết quả (giả định)
# Start A
# Start B
# End A
# End B
# Done
# 👉 A và B chạy song song
```
## Pool
```bash
Dùng khi bạn có nhiều task giống nhau
```
# Display (cung cấp thông tin)
## cpu_count()
```bash
lấy số core cp
```
**Ex**
```python
from multiprocessing import cpu_count

print(cpu_count()) # 8
```
# Process (xử lý)
## .map
**Syn**
```bash
Pool(n).map(func, iterable)
```
**Ex**
```python
from multiprocessing import Pool

def square(x):
    return x * x

if __name__ == "__main__":
    with Pool(4) as p:
        result = p.map(square, [1, 2, 3, 4])

    print(result)

# [1, 4, 9, 16]
```
## .apply()
```bash
Dùng để chạy 1 task
```
**Syn**
```bash
p.apply(func, args=(...))
```
**Ex**
```python
from multiprocessing import Pool

def add(a, b):
    return a + b

if __name__ == "__main__":
    with Pool(2) as p:
        result = p.apply(add, args=(2, 3))

    print(result)

# 5
```
## apply_async()
```bash
Bất đồng bộ
```
**Syn**
```bash
result = p.apply_async(func, args=(...))
result.get()
```
**Ex**
```python
from multiprocessing import Pool

def square(x):
    return x * x

if __name__ == "__main__":
    with Pool(2) as p:
        res = p.apply_async(square, args=(5,))
        print("Doing other work...")
        print(res.get())

# Doing other work...
# 25
```
## .imap()
```bash
trả kết quả dần dần
```
## Queue()
### .put()
**Ex**
```bash
from multiprocessing import Process, Queue

def worker(q):
    q.put("Hello from process")

if __name__ == "__main__":
    q = Queue()

    p = Process(target=worker, args=(q,))
    p.start()
    print(q.get())

    p.join()
```
