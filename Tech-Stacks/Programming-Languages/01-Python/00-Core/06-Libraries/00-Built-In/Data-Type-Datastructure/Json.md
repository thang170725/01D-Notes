- [.load() (dùng để đọc json từ file)](#load-dùng-để-đọc-json-từ-file)
- [.loads() (dùng để chuyển một chuỗi JSON (str) thành object Python)](#loads-dùng-để-chuyển-một-chuỗi-json-str-thành-object-python)
- [.dump() (dùng để ghi dữ liệu ra file json)](#dump-dùng-để-ghi-dữ-liệu-ra-file-json)
- [dumps() (chuyển python object -\> chuỗi json)](#dumps-chuyển-python-object---chuỗi-json)
---
# .load() (dùng để đọc json từ file)
**Ex**
```python
import json

with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)

print(data)
```
# .loads() (dùng để chuyển một chuỗi JSON (str) thành object Python)
**Ex**
```python
import json

data = '{"name": "Thang", "age": 30}'
result = json.loads(data)

print(result) # {'name': 'Thang', 'age': 30}
print(type(result)) # <class 'dict'>
```
**Ex2: JSON array → Python list**
```python
import json

data = '[{"id": 1, "name": "A"}, {"id": 2, "name": "B"}]'

result = json.loads(data)

print(result)
print(type(result))
# [
#     {"id": 1, "name": "A"},
#     {"id": 2, "name": "B"}
# ]
# <class 'list'>
```
# .dump() (dùng để ghi dữ liệu ra file json)
**Syn**
```bash
json.dump(
    email_channel_data,
    f,
    ensure_ascii=False,
    indent=4
)

- Input:
    + indent=4: Nó quy định số khoảng trắng để thụt đầu dòng (indentation) khi ghi JSON.
```
```python
import json

data = {
    "name": "Thang",
    "age": 20,
    "skills": ["Python", "AI"]
}

with open("output.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=4)
```
# dumps() (chuyển python object -> chuỗi json)
**Syn**
```bash
json.dumps(obj, *, skipkeys=False, ensure_ascii=True,
           check_circular=True, allow_nan=True,
           cls=None, indent=None, separators=None,
           default=str, sort_keys=False, **kw)

- Input:
    + skipkeys=bool:
        - False: key không hợp lệ -> báo lỗi
        - True: key không hợp lệ -> bỏ qua
    + ensure_ascii=bool:
        - True  → Unicode → \uXXXX
        - False → giữ nguyên Unicode
    + default=any: Nếu gặp một object mà JSON không biết xử lý thì phải chuyển nó như thế nào?
        - str: chuyển về string
```
**Ex**
```python
import json

data = {
    "name": "Thắng",
    "age": 20
}

result = json.dumps(data)

print(result) # {"name": "Thắng", "age": 20}
```