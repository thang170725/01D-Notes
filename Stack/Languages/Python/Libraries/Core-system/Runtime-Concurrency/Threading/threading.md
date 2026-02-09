Threading
    • Threading là đa luồng giúp chạy nhiều luồng song song trong một process. Ví dụ: đọc video + xử lý AI song song → nhanh hơn.
Thread()
Cú pháp:
t = threading.Thread(target=func, args=(a,b,c))
    • args: là tuple các tham số được truyền vào hàm target. tương đương với func(a, b, c)
.start()
Kích hoạt thread để chạy hàm target
Cú pháp:
import threading
import time

def threading1():
    print(f'the threading 1 is starting ...')
    time.sleep(5)
    print(f'the threading 1 is ending ...')

def threading2():
    print(f'the threading 2 is starting ...')
    time.sleep(5)
    print(f'the threading 2 is ending ...')

threading.Thread(target=threading1).start()
threading.Thread(target=threading2).start()
the threading 1 is starting ...
the threading 2 is starting ...
the threading 1 is ending ...
the threading 2 is ending …
# nếu không có threading nó sẽ chạy kiểu này
the threading 1 is starting ...
the threading 1 is ending ...
the threading 2 is starting ...
the threading 2 is ending …

Threading không chạy song song:
import threading
import time

def cpu_task():
    s = 0
    for i in range(100_000_000):
        s += i

start = time.time()

t1 = threading.Thread(target=cpu_task)
t2 = threading.Thread(target=cpu_task)

t1.start()
t2.start()

t1.join()
t2.join()

print("Time:", time.time() - start)
Time: 13.588137149810791
# đối với phần tính toán threading không thật sự chạy song song

from multiprocessing import Process
import time

def cpu_task():
    s = 0
    for i in range(100_000_000):
        s += i

start = time.time()

p1 = Process(target=cpu_task)
p2 = Process(target=cpu_task)

p1.start()
p2.start()

p1.join()
p2.join()

print("Time:", time.time() - start)
Time: 7.604533910751343

.join()
Chờ thread chạy xong
Cú pháp:
import threading
import time

def worker():
    print("Thread bắt đầu")
    time.sleep(1)
    print("Thread kết thúc")

t = threading.Thread(target=worker)
t.start()
t.join()
print("Tất cả đã xong!")
Thread bắt đầu
Thread kết thúc
Tất cả đã xong!
.is_alive()
Kiểm tra thread còn chạy không
Cú pháp:
t = threading.Thread(target=worker)
t.start()

print(t.is_alive())  # True
t.join()
print(t.is_alive())  # False
True
False
.daemon
current_thread()
Trả về thread hiện tại
Cú pháp:
def worker():
    print("Đang chạy ở:", threading.current_thread().name)

thread = threading.Thread(target=worker, name="Worker-1")
thread.start()
Đang chạy ở: Worker-1
active_count()
Lock()
Event()
Semaphore()
Timer()