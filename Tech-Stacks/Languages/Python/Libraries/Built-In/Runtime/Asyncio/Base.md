- [coroutine](#coroutine)
- [async \& await](#async--await)
- [.sleep() \& .gather() \& .run()](#sleep--gather--run)
  - [Bài tập](#bài-tập)
    - [Nhận diện và sửa code bị block event loop](#nhận-diện-và-sửa-code-bị-block-event-loop)
- [create\_task()](#create_task)
  - [Bài tập](#bài-tập-1)
    - [Sự khác biệt khi dùng và không dùng create\_task](#sự-khác-biệt-khi-dùng-và-không-dùng-create_task)
    - [Sự khác biệt của create\_task \& gather](#sự-khác-biệt-của-create_task--gather)
    - [Khi gather không đủ bắt buộc phải dùng create\_task](#khi-gather-không-đủ-bắt-buộc-phải-dùng-create_task)
  - [.cancel() \& .CancelledError()](#cancel--cancellederror)
    - [Demo chuẩn luồng hoạt động cơ bản](#demo-chuẩn-luồng-hoạt-động-cơ-bản)
- [.Queue() \& .put() \& .get() \& task\_done() \& .join()](#queue--put--get--task_done--join)
  - [Bài tập](#bài-tập-2)
    - [Demo](#demo)


---

**Khái niệm**
- Giúp chương trình xử lý nhiều tác vụ cùng lúc mà không cần phải chờ từng tác vụ hoàn thành trước khi chuyển sang tác vụ tiếp theo.
- Chỉ dùng cho I/O không dùng cho CPU-bound.
- Thư viện không cần tải.

# coroutine
- Hàm có thể tạm dừng và tiếp tục
- Coroutine ≠ Thread
  + Thread = chạy song song thật, có CPU riêng.
  + Coroutine = chạy “từng bước một”, nhưng chia sẻ cùng 1 thread.
  + Không cần thread, không tốn CPU nhiều, nhưng vẫn làm được nhiều việc tưởng song song nhờ await.
**Normal**
```python
def f():
    print("A")
    print("B")
f()
# Khi gọi f(), hàm chạy liền và không bao giờ dừng cho đến khi xong.
```
**Use coroutine**
```python
async def f():
    print("A")

coro = f()
print(coro)
# <coroutine object f at 0x...>
# Chưa chạy gì cả! Nó chỉ tạo ra một “việc cần làm”.
```

# async & await
- await: Tạm nhường quyền điều khiển cho even loop (even loop là người điều phối chương trình)
- Coroutine + Await
  + await chỉ có nghĩa với coroutine hoặc các object awaitable.
  + Khi bạn await một coroutine:
    + Coroutine hiện tại tạm dừng
    + Event loop có thể chạy coroutine khác
    + Khi xong, tiếp tục coroutine ban đầu
```python
async def f():
    for i in range(3):
        print("before", i)
        await asyncio.sleep(0)
        print("after", i)
# Mỗi lần gặp await, Python dừng f, nhường quyền cho event loop chạy việc khác.
# Khi xong, f tiếp tục từ đúng dòng đó, i vẫn giữ nguyên.
```
# .sleep() & .gather() & .run()

- gather: Gom lại để event loop quản lý cùng lúc
**Ví dụ**
```python
import asyncio

async def task_a():
    print('a start')
    await asyncio.sleep(2) # tạm dừng coroutine hiện tại và trả quyền điều khiển cho event loop
    print('a end')

async def task_b():
    print('b start')
    await asyncio.sleep(2) 
    print('b end')

async def main():
    await asyncio.gather( 
        task_a(),
        task_b()
    )

if __name__ == "__main__":
    asyncio.run(main())
```
## Bài tập
### Nhận diện và sửa code bị block event loop
**code bị block**
```python

```

# create_task()
đăng ký cho event loop chạy nền
## Bài tập
### Sự khác biệt khi dùng và không dùng create_task
**Not use**
```python
import asyncio
import time

async def send_log():
    print("Start sending log")
    await asyncio.sleep(3)
    print("Log sent")

async def main():
    start = time.time()

    print("Do work 1")
    await send_log()              # ❌ BỊ CHẶN 3 GIÂY
    print("Do work 2")

    print("Total:", time.time() - start)

asyncio.run(main())

# Do work 1
# Start sending log
# (Log chờ 3 giây)
# Log sent
# Do work 2
# Total: ~3s
# Vấn đề: Bạn bị buộc phải chờ log gửi xong mới làm việc tiếp.
```
**Use**
```python
import asyncio
import time

async def send_log():
    print("Start sending log")
    await asyncio.sleep(3)
    print("Log sent")

async def main():
    start = time.time()

    print("Do work 1")
    task = asyncio.create_task(send_log())  # ✅ chạy nền
    print("Do work 2")

    await task  # chờ kết thúc ở thời điểm mình CHỌN

    print("Total:", time.time() - start)

asyncio.run(main())

# Do work 1
# Start sending log
# Do work 2
# (Log chạy nền 3 giây)
# Log sent
# Total: ~3s
```

### Sự khác biệt của create_task & gather
**use gather**
```python
import asyncio
import time

async def send_log():
    print("log: start")
    await asyncio.sleep(3)
    print("log: done")

async def do_work():
    print("work: start")
    await asyncio.sleep(1)
    print("work: done")

async def main():
    start = time.time()

    await asyncio.gather(
        send_log(),
        do_work()
    )

    print("Total:", time.time() - start)

asyncio.run(main())
# Vấn đề gather BẮT BUỘC chờ TẤT CẢ. Bạn không thể làm việc khác sau work xong. gather = “làm cùng lúc nhưng đợi hết”
```
**use create_task**
```python
async def main():
    start = time.time()

    log_task = asyncio.create_task(send_log())  # chạy nền

    await do_work()                             # KHÔNG bị chặn

    print("work finished, doing something else")

    await log_task                              # đợi KHI MÌNH MUỐN

    print("Total:", time.time() - start)

# create_task cho phép bạn TÁCH thời điểm “chạy” và “đợi”
```

### Khi gather không đủ bắt buộc phải dùng create_task
**use gather**
```python
import asyncio

async def ticker():
    while True:
        print('tick')
        await asyncio.sleep(1)

async def background_job():
    print('job start')
    await asyncio.sleep(5)
    print('job done')

async def main():
    await asyncio.gather(
        ticker(),
        background_job()
    )

if __name__ == '__main__':
    asyncio.run(main())
```
**use create_task**
```python
import asyncio

async def ticker():
    try:
        while True:
            print("tick")
            await asyncio.sleep(1)
    except asyncio.CancelledError:
        print("ticker cancelled")

async def background_job():
    print("job start")
    await asyncio.sleep(5)
    print("job done")

async def main():
    # 1️⃣ Khởi động task vô hạn (KHÔNG await)
    ticker_task = asyncio.create_task(ticker())

    # 2️⃣ Khởi động background job
    job_task = asyncio.create_task(background_job())

    # 3️⃣ Main tiếp tục chạy ngay
    print("main continues")

    # 4️⃣ Chỉ đợi task HỮU HẠN
    await job_task

    # 5️⃣ Dọn dẹp task vô hạn
    ticker_task.cancel()
    await ticker_task

if __name__ == "__main__":
    asyncio.run(main())
```

## .cancel() & .CancelledError()
- hủy một task đang chạy
- Khi bạn call task.cancel() → task ném asyncio.CancelledError vào coroutine
- Coroutine có thể try/except bắt để cleanup trước khi thoát
```python
task = asyncio.create_task(worker())
# Hủy task
task.cancel()
try:
    await task
except asyncio.CancelledError:
    print("Task was cancelled gracefully")
```
### Demo chuẩn luồng hoạt động cơ bản
```python
import asyncio

async def producer(queue: asyncio.Queue):
    for job in range(10):
        await queue.put(job)
        print(f'produced {job}')

async def consumer(queue: asyncio.Queue, id: int):
    while True:
        job = await queue.get()
        if job is None:  # poison pill
            queue.task_done()
            break
        print(f'worker-{id} processing {job}')
        await asyncio.sleep(1)  # mô phỏng I/O
        queue.task_done()

async def main():
    queue = asyncio.Queue(maxsize=3)

    # tạo 3 worker
    workers = [asyncio.create_task(consumer(queue, i)) for i in range(3)]

    # producer tạo job
    await producer(queue)

    # thêm poison pill cho mỗi worker
    for _ in range(3):
        await queue.put(None)

    # chờ tất cả job xong
    await queue.join()

    # chờ tất cả worker dừng
    for w in workers:
        await w

    print("all jobs processed and workers stopped")

if __name__ == '__main__':
    asyncio.run(main())
```
# .Queue() & .put() & .get() & task_done() & .join()
- Queue     : Là công cụ điều phối giữa các task.
- task_done : Chỉ dùng với asyncio.Queue, nghĩa là việc lấy ra ở get đã được xử lý xong hoàn toàn. Mỗi get() BẮT BUỘC có 1 task_done() tương ứng
    ```python
    item = await queue.get() # xử lý item
    queue.task_done()
    ```
- join      : Đợi cho đến khi TẤT CẢ item đã put vào queue được xử lý xong (task_done)” join KHÔNG quan tâm còn consumer chạy hay không. Nó chỉ quan tâm việc đã xong chưa.
**Flow Chart**
```bash
Producer:
  await queue.put(item)
                ↓
          ┌─────────────┐
          │   asyncio   │
          │    Queue    │
          └─────────────┘
                ↓
Consumer:
  item = await queue.get()
  process(item)
  queue.task_done()

Main:
  await queue.join()
```
**Syn**
```bash
queue = asyncio.Queue(maxsize=3)
- maxsize: số phần tử tối đa trong queue
```
**Ex**
```python
import asyncio

async def producer(queue):
    for i in range(5):
        print("produce", i)
        await queue.put(i)
    print("producer done")

async def consumer(queue):
    while True:
        item = await queue.get()
        print("consume", item)
        queue.task_done()

async def main():
    queue = asyncio.Queue()

    asyncio.create_task(consumer(queue))
    await producer(queue)

    await queue.join()
    print("all tasks done")

asyncio.run(main())
```
**Ex**
```python
import asyncio

queue = asyncio.Queue(maxsize=3)

async def producer(name):
    for i in range(3):
        await queue.put(f"{name}-{i}")
        print(f"Produced {name}-{i}")
        await asyncio.sleep(1)

async def consumer(name):
    while True:
        item = await queue.get()
        print(f"Consumer {name} got {item}")
        await asyncio.sleep(2)
        queue.task_done()

async def main():
    producers = [
        asyncio.create_task(producer("P1")),
        asyncio.create_task(producer("P2")),
    ]

    consumers = [
        asyncio.create_task(consumer("C1")),
        asyncio.create_task(consumer("C2")),
    ]

    await asyncio.gather(*producers)
    await queue.join()

    for c in consumers:
        c.cancel()

asyncio.run(main())
```
## Bài tập
### Demo
```python 
import asyncio

async def producter(queue: asyncio.Queue):
    for job in range(10):
        await queue.put(job)
        print(f'produced {job}')

async def consumer(queue: asyncio.Queue, worker_id: int):
    while True:
        job = await queue.get()
        print(f'worker-{worker_id} processing {job}')
        await asyncio.sleep(1)
        queue.task_done()

async def main():
    queue = asyncio.Queue(maxsize=3)

    for i in range(3):
        asyncio.create_task(consumer(queue=queue, worker_id=i))

    await producter(queue=queue)

    await queue.join()
    print('all jobs processed')


if __name__ == '__main__':
    asyncio.run(main())
```