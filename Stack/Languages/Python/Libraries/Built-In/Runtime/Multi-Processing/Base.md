Multiprocessing
Process()
p = mp.Process(target=func, args=(a, b))
.start()
.join()
Queue()
.put & .get()
def producer(q):
    for i in range(5):
        q.put(i)

def consumer(q):
    while True:
        item = q.get()
        print("Got:", item)

if __name__ == "__main__":
    q = mp.Queue()
    mp.Process(target=producer, args=(q,)).start()
    mp.Process(target=consumer, args=(q,)).start()
