- [.load() (dùng để đọc json từ file)](#load-dùng-để-đọc-json-từ-file)
- [.loads() (đọc json từ chuỗi)](#loads-đọc-json-từ-chuỗi)
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
# .loads() (đọc json từ chuỗi)
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