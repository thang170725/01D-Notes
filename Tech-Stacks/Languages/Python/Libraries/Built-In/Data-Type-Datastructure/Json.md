- [.load () (dung de load mot file json vao python)](#load--dung-de-load-mot-file-json-vao-python)
- [.dump() ()](#dump-)
---
# .load () (dùng để load file json vào python)
**Ex**
```python
import json

with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)

print(data)
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