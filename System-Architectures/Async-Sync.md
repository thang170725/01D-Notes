+ [<<Back](Base.md)
- [Sync Introduction (synchronous là làm tuần tự, việc A xong mới làm B)](#sync-introduction-synchronous-là-làm-tuần-tự-việc-a-xong-mới-làm-b)
- [Async Introduction (asynchronous có thể bắt đầu việc khác trong lúc chờ A)](#async-introduction-asynchronous-có-thể-bắt-đầu-việc-khác-trong-lúc-chờ-a)
---
# Sync Introduction (synchronous là làm tuần tự, việc A xong mới làm B)
**Ex: Ví dụ bạn gọi API**
```bash
data = requests.get(url)   # chờ server trả về
print(data)
print("Done")

Luồng chạy: Gọi API -> CHỜ API trả về -> Nhận data -> print -> Done
    Nếu API mất 5 giây thì chương trình đứng chờ 5 giây ở đó. -> Đây là sync.
```
**Khi nào dùng Sync?**
```bash
Dùng sync khi công việc của bạn chủ yếu đơn giản hoặc không cần chạy đồng thời:
    - Đọc một file
    - Xử lý một JSON
    - Tính toán
    - Chạy pipeline tuần tự
    - Code script nhỏ
    - Các bước phụ thuộc nhau
```
# Async Introduction (asynchronous có thể bắt đầu việc khác trong lúc chờ A)
```bash
Trong lúc đang chờ một tác vụ I/O, chương trình có thể xử lý việc khác.
```
**Ex**
```bash
async def get_data():
    data = await fetch_data() # "Việc này đang chờ kết quả. Trong lúc chờ, nếu có việc khác thì cứ làm đi."
    print(data)
```
**Ex2: Ví dụ có 3 API:**
```bash
API A ──────── 5s
API B ── 2s
API C ─── 3s

Sync:
    A █████ 5s
              B ██ 2s
                    C ███ 3s
-> Tổng ≈ 10s

Async:
    A █████
    B ██
    C ███
-> Tổng ≈ 5s
```
**Khi nào dùng Async?**
```bash
Async đặc biệt hữu ích khi chương trình phải chờ I/O nhiều.
    - Gọi API
    - Gọi API
    - Gọi API
    - Đọc network
    - Đợi database
    - Đợi database
```