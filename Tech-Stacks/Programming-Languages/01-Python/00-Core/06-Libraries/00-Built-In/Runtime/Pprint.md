pprint trong Python là viết tắt của pretty print, dùng để in dữ liệu ra màn hình theo dạng dễ đọc hơn, đặc biệt hữu ích với dict, list hoặc JSON lồng nhau.

1. Cú pháp cơ bản
from pprint import pprint

pprint(data)

Ví dụ:

from pprint import pprint

data = {
    "name": "Thang",
    "age": 25,
    "skills": ["Python", "AI", "SQL"]
}

pprint(data)

Kết quả có thể là:

{'age': 25,
 'name': 'Thang',
 'skills': ['Python', 'AI', 'SQL']}

So với:

print(data)

thì:

{'name': 'Thang', 'age': 25, 'skills': ['Python', 'AI', 'SQL']}

pprint() sẽ tự format và xuống dòng để dễ nhìn hơn.

2. Rất hữu ích với dữ liệu nested

Ví dụ dữ liệu JSON của bạn có dạng:

data = {
    "document": {
        "id": "ABC123",
        "pages": [
            {
                "page": 1,
                "items": [
                    {"text": "Hello", "x": 10, "y": 20},
                    {"text": "World", "x": 30, "y": 40}
                ]
            },
            {
                "page": 2,
                "items": [
                    {"text": "Python", "x": 50, "y": 60}
                ]
            }
        ]
    }
}

Dùng:

from pprint import pprint

pprint(data)

sẽ dễ đọc hơn rất nhiều so với print(data).

3. pprint() có một số tham số hay dùng

Cú pháp đầy đủ thường gặp:

pprint(object, indent=1, width=80, depth=None)
width

Quy định độ rộng tối đa trước khi pprint xuống dòng.

pprint(data, width=120)

Ví dụ dữ liệu dài, width=120 sẽ giúp nó ít xuống dòng hơn.

indent

Điều chỉnh độ thụt đầu dòng:

pprint(data, indent=4)

Ví dụ:

{'document': {'id': 'ABC',
              'pages': [{'page': 1,
                         'items': [...] }]}}
depth

Giới hạn độ sâu muốn hiển thị:

pprint(data, depth=2)

Ví dụ dữ liệu quá sâu:

{'document': {'id': 'ABC',
              'pages': [...]}}

Thay vì in toàn bộ bên trong pages.

4. Một cách dùng rất hay khi debug

Trong code của bạn, nếu muốn xem JSON đang thực sự có cấu trúc như thế nào, có thể:

from pprint import pprint

pprint(raw_data)

Hoặc:

pprint(raw_data, depth=3)

Ví dụ bạn đang không biết raw_data là dict, list hay str:

print(type(raw_data))
pprint(raw_data)

Kết quả:

<class 'dict'>

{'OCR_IMAGE_ID': '12345',
 'RAW_DATA': '{"data": [...]}',
 'STATUS': 'OK'}

Cách này đặc biệt hữu ích khi debug lỗi kiểu:

TypeError: string indices must be integers

vì bạn có thể nhìn trực tiếp cấu trúc dữ liệu thay vì đoán.

Nhớ đơn giản:
print(data)          # in bình thường
pprint(data)         # in đẹp, dễ đọc
type(data)           # xem kiểu dữ liệu

pprint chỉ giúp hiển thị, nó không thay đổi dữ liệu gốc.