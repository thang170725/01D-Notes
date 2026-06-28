# Counter()
Tham số truyền vào có thể là list, tuple, ...
**Ex**
```python
from collections import Counter

c = Counter(['a', 'b', 'a', 'c', 'b', 'a'])
print(c)
# Counter({'a': 3, 'b': 2, 'c': 1})
```

# .values()
```python
from collections import Counter
c = Counter(['a', 'b', 'c', 'a'])
print(c.values())

# dict_values([2, 1, 1])
```
.most_common()
Trả về n phần tử xuất hiện nhiều nhất.
Cú pháp:
c = Counter("aaabbbbccdde")
print(c.most_common(2)) # Nếu không truyền n → trả tất cả theo thứ tự giảm dần.
[('b', 4), ('a', 3)]
.elements()
Trả ra tất cả phần tử, lặp lại theo số lần đếm.
Cú pháp:
c = Counter({'a': 2, 'b': 3})
print(list(c.elements()))
['a', 'a', 'b', 'b', 'b']
.update()
Giống như cộng thêm dữ liệu mới.
Cú pháp:
c = Counter("abc")
c.update("aba")   # thêm a,b,a
print(c)
Counter({'a': 3, 'b': 2, 'c': 1})
.subtract()
Không xóa phần tử, chỉ giảm số lượng (có thể âm).
Cú pháp:
c = Counter("aabbb")
c.subtract("abb")
print(c)
Counter({'b': 2, 'a': 1})
[]
c = Counter("aabbc")
print(c['a'])  # 2
print(c['x'])  # 0, không có thì trả 0
+
c1 = Counter(a=3, b=1)
c2 = Counter(a=1, b=3)
print(c1 + c2)
Counter({'a': 4, 'b': 4})
-
c1 = Counter(a=4, b=2)
c2 = Counter(a=3, b=5)
print(c1 - c2)
Counter({'a': 1})
& (Lấy MIN theo key)
c1 = Counter(a=4, b=2)
c2 = Counter(a=3, b=5)
print(c1 & c2)
Counter({'a': 3, 'b': 2})
| (Lấy max theo key)
.clear()
del
Counter từ dict / tuple list
Thực ra từ Python 3.7+, dict đã giữ nguyên thứ tự insert, nên trong 90% trường hợp bạn không cần dùng OrderedDict nữa.

OrderedDict chỉ còn hữu ích khi bạn cần các thao tác đặc biệt như:

di chuyển phần tử lên đầu/cuối (move_to_end)
xóa phần tử đầu/cuối (popitem(last=False))
cần tương thích với code cũ.
1. Khởi tạo
from collections import OrderedDict

data = OrderedDict()

Hoặc

from collections import OrderedDict

data = OrderedDict([
    ("a", 1),
    ("b", 2),
    ("c", 3)
])

print(data)

Kết quả

OrderedDict([
    ('a', 1),
    ('b', 2),
    ('c', 3)
])
2. Thêm phần tử

Giống dict

from collections import OrderedDict

data = OrderedDict()

data["apple"] = 10
data["banana"] = 20
data["orange"] = 30

print(data)

Kết quả

OrderedDict([
    ('apple', 10),
    ('banana', 20),
    ('orange', 30)
])
3. Duyệt
for key, value in data.items():
    print(key, value)
apple 10
banana 20
orange 30
4. Truy cập
print(data["banana"])
20
5. Kiểm tra tồn tại
if "apple" in data:
    print("Có")
6. Cập nhật
data["banana"] = 100
7. Xóa
del data["apple"]
8. move_to_end()

Đây là chức năng mà dict không có.

Ví dụ

from collections import OrderedDict

data = OrderedDict()

data["A"] = 1
data["B"] = 2
data["C"] = 3

print(data)
A B C

Đưa A xuống cuối

data.move_to_end("A")

print(data)
B C A

Hoặc đưa lên đầu

data.move_to_end("C", last=False)

print(data)
C B A
9. popitem()
dict
d.popitem()

luôn xóa cuối.

OrderedDict

Xóa cuối

data.popitem()
('A',1)

Hoặc xóa đầu

data.popitem(last=False)

Ví dụ

A B C D
data.popitem(last=False)

còn

B C D
10. Ví dụ thực tế (group query SQL)

Đây là trường hợp bạn sẽ gặp nhiều trong FastAPI.

Query trả về

rows = [
    {
        "exercise_id":1,
        "exercise_name":"Bench",
        "set_number":1
    },
    {
        "exercise_id":1,
        "exercise_name":"Bench",
        "set_number":2
    },
    {
        "exercise_id":2,
        "exercise_name":"Squat",
        "set_number":1
    }
]

Muốn group

from collections import OrderedDict

exercise_map = OrderedDict()

for row in rows:

    exercise_id = row["exercise_id"]

    if exercise_id not in exercise_map:

        exercise_map[exercise_id] = {
            "exercise_id": exercise_id,
            "exercise_name": row["exercise_name"],
            "sets": []
        }

    exercise_map[exercise_id]["sets"].append({
        "set_number": row["set_number"]
    })

result = list(exercise_map.values())

print(result)

Kết quả

[
    {
        "exercise_id":1,
        "exercise_name":"Bench",
        "sets":[
            {"set_number":1},
            {"set_number":2}
        ]
    },
    {
        "exercise_id":2,
        "exercise_name":"Squat",
        "sets":[
            {"set_number":1}
        ]
    }
]

Đây chính là pattern rất phổ biến để chuyển dữ liệu SQL (1 dòng cho mỗi set) thành JSON lồng nhau.

11. So sánh với dict

Hiện nay bạn có thể viết y hệt bằng dict:

exercise_map = {}

for row in rows:
    exercise_id = row["exercise_id"]

    if exercise_id not in exercise_map:
        exercise_map[exercise_id] = {
            "exercise_id": exercise_id,
            "exercise_name": row["exercise_name"],
            "sets": []
        }

    exercise_map[exercise_id]["sets"].append({
        "set_number": row["set_number"]
    })

result = list(exercise_map.values())

Kết quả giống hệt OrderedDict trên Python 3.7+.

Khi nào nên dùng cái nào?
dict: lựa chọn mặc định cho hầu hết mọi trường hợp hiện nay.
OrderedDict: dùng khi bạn cần các thao tác đặc biệt như move_to_end() hoặc popitem(last=False), hoặc đang làm việc với code cũ yêu cầu OrderedDict.

Đối với các service FastAPI/SQLAlchemy như bạn đang viết để group dữ liệu từ database thành JSON, dict là đủ và được khuyến nghị.
# Defaultdict
**Syn**
```python
from collections import defaultdict

class BFS:
    def __init__(self):
        self.data = defaultdict(list)

    def tree_data(self):
        # Khởi tạo dữ liệu cây dạng dictionary (adjacency list)
        self.data['A'] = ['B', 'C', 'D']
        self.data['B'] = ['M', 'N']
        self.data['C'] = ['L']
        self.data['D'] = ['O', 'P']
        self.data['M'] = ['X', 'Y']
        self.data['N'] = ['U', 'V']
        self.data['O'] = ['I', 'J']
        self.data['Y'] = ['R', 'S']
        self.data['V'] = ['G', 'H']
        return self.data

if __name__ == '__main__':
    bfs = BFS()
    print(bfs.tree_data())
# defaultdict(<class 'list'>, {'A': ['B', 'C', 'D'], 'B': ['M', 'N'], 'C': ['L'], 'D': ['O', 'P'], 'M': ['X', 'Y'], 'N': ['U', 'V'], 'O': ['I', 'J'], 'Y': ['R', 'S'], 'V': ['G', 'H']})
```
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