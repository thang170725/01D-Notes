- [Ijson Introduction (dùng để đọc JSON theo kiểu streaming, tức là không cần json.load() toàn bộ file vào RAM)](#ijson-introduction-dùng-để-đọc-json-theo-kiểu-streaming-tức-là-không-cần-jsonload-toàn-bộ-file-vào-ram)
- [Installation](#installation)
- [.items()](#items)
---
# Ijson Introduction (dùng để đọc JSON theo kiểu streaming, tức là không cần json.load() toàn bộ file vào RAM)
```bash
Điều này rất hữu ích nếu JSON của bạn rất lớn, ví dụ vài GB hoặc hàng triệu object.
```
# Installation
```bash
pip install ijson
```
# .items()
**Không dùng ijson**
```bash
Ví dụ JSON:
[
    {"id": 1, "name": "A"},
    {"id": 2, "name": "B"},
    {"id": 3, "name": "C"}
]
```
```python
import json

with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)


for item in data:
    print(item)

# json.load() sẽ đọc toàn bộ JSON vào RAM.
```
**Dùng ijson**
```python
import ijson

with open("data.json", "rb") as f:
    for item in ijson.items(f, "item"):
        print(item)

# Lúc này:
#     file JSON
#        │
#        ▼
#     ijson
#        │
#        ├── object 1 → xử lý
#        ├── object 2 → xử lý
#        ├── object 3 → xử lý
#        └── ...
# Không cần load toàn bộ file.
```
1. Trường hợp quan trọng nhất: JSON là list

Ví dụ file của bạn:

[
    {
        "id": "001",
        "name": "Nguyen Van A"
    },
    {
        "id": "002",
        "name": "Nguyen Van B"
    }
]

Dùng:

import ijson


with open("data.json", "rb") as f:
    for item in ijson.items(f, "item"):
        print(item["id"])
        print(item["name"])

"item" nghĩa là:

Lấy từng phần tử bên trong list ở root.

4. JSON của bạn có dạng object

Ví dụ:

{
    "hoadon": {
        "patient_name": "ABC",
        "patient_code": "123"
    },
    "giayravien": {
        "patient_name": "DEF",
        "patient_code": "456"
    }
}

Có thể đọc:

import ijson


with open("data.json", "rb") as f:
    for key, value in ijson.kvitems(f, ""):
        print(key)
        print(value)

Kết quả:

hoadon
{'patient_name': 'ABC', 'patient_code': '123'}


giayravien
{'patient_name': 'DEF', 'patient_code': '456'}
5. Đọc sâu vào JSON

Ví dụ:

{
    "documents": [
        {
            "id": "001",
            "type": "hoadon",
            "fields": {
                "name": "ABC",
                "address": "Ha Noi"
            }
        },
        {
            "id": "002",
            "type": "giayravien",
            "fields": {
                "name": "DEF"
            }
        }
    ]
}

Bạn muốn đọc từng document:

import ijson


with open("data.json", "rb") as f:
    for document in ijson.items(f, "documents.item"):
        print(document)

documents.item nghĩa là:

root
 └── documents
      ├── item 1
      ├── item 2
      └── item 3
6. Đặc biệt hữu ích với dữ liệu 3000 folder của bạn

Ví dụ mỗi folder có:

51c6.../
├── page_mapping.json
├── page_group_mapping.json
└── type_text_mapping.json

Nếu một type_text_mapping.json rất lớn, thay vì:

with open(path, encoding="utf-8") as f:
    data = json.load(f)

bạn có thể:

import ijson


with open(path, "rb") as f:
    for group_id, fields in ijson.kvitems(f, ""):
        if group_id == "id":
            continue


        print(group_id)
        print(fields)

Như vậy bạn xử lý từng group thay vì load toàn bộ file.

7. Nhưng có một điểm rất quan trọng

ijson không phải lúc nào cũng tốt hơn json.load().

Nếu file của bạn chỉ:

500 KB
2 MB
10 MB

thì:

json.load()

thường đơn giản và đủ nhanh.

ijson bắt đầu đặc biệt có giá trị khi:

JSON rất lớn
        +
RAM hạn chế
        +
chỉ cần xử lý từng phần
Với project của bạn

Bạn đang quét 3000 folder, mỗi folder có 3 JSON.

Nếu vấn đề của bạn là:

"3000 folder chạy lâu, sợ crash giữa chừng"

thì ijson không giải quyết trực tiếp vấn đề đó.

Cái quan trọng hơn vẫn là kiến trúc:

3000 folders
      │
      ▼
batch 200 folders
      │
      ▼
xử lý
      │
      ▼
save checkpoint
      │
      ▼
batch tiếp theo

Còn ijson hữu ích nếu một trong các JSON bên trong mỗi folder quá lớn.

Ví dụ pipeline của bạn có thể kết hợp:

3000 folders
      │
      ├── batch 200
      │
      ├── folder 1
      │    ├── ijson → page_mapping
      │    ├── ijson → page_group
      │    └── ijson → type_text
      │
      ├── folder 2
      │
      └── ...

Nếu 3 file JSON của bạn mỗi file chỉ vài KB/MB thì chưa cần đổi sang ijson; checkpoint + batch 200 sẽ có lợi hơn nhiều.

Tiếp tục tìm hiểu:

Dùng ijson với JSON lồng nhiều tầng
Kết hợp ijson với checkpoint theo batch