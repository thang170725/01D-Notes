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