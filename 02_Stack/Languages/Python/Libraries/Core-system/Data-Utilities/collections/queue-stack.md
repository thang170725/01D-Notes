# deque
Phiên bản “xịn” của list để làm queue/stack. List pop(0) = O(n) (chậm). deque popleft() = O(1) (cực nhanh).
**Syn**
```bash
window = deque(maxlen=3)
```
```python
from collections import deque

window = deque(maxlen=3)  # tối đa 3 phần tử

for i in range(1, 7):
    window.append(i)
    print(list(window))
# [1]
# [1, 2]
# [1, 2, 3]
# [2, 3, 4]
# [3, 4, 5]
# [4, 5, 6]
```

# .popleft()
Thường dùng trong hàng đợi.
**Syn**
```python
from collections import deque

q = deque()

q.append("A")
q.append("B")
q.append("C")

print(q.popleft())  # A
print(q.popleft())  # B
```

# .pop()
Thường dùng trong ngăn xếp.
Cú pháp:
stack = deque()

stack.append(1)
stack.append(2)
stack.append(3)

print(stack.pop())   # 3
print(stack.pop())   # 2