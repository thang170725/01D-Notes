- [Argparse Introduction (dùng để xử lý tham số từ command line/terminal khi chạy chương trình)](#argparse-introduction-dùng-để-xử-lý-tham-số-từ-command-lineterminal-khi-chạy-chương-trình)
- [ArgumentParser (class dùng để tạo một bộ phân tích command-line arguments)](#argumentparser-class-dùng-để-tạo-một-bộ-phân-tích-command-line-arguments)
  - [.add\_argument() (dùng để nói cho chương trình biết command-line của chương trình nhận những tham số nào kiểu gì mặc định là gì bắt buộc hay không)](#add_argument-dùng-để-nói-cho-chương-trình-biết-command-line-của-chương-trình-nhận-những-tham-số-nào-kiểu-gì-mặc-định-là-gì-bắt-buộc-hay-không)
  - [.parse\_args()](#parse_args)
    - [.name](#name)
---
# Argparse Introduction (dùng để xử lý tham số từ command line/terminal khi chạy chương trình)
```bash
argparse là standard library của Python. 
    - Bạn chỉ cần: import argparse 
    - Không cần: pip install argparse

Nó rất hữu ích để biến một file Python thành kiểu:
    python train.py --model yolov8n.pt --epochs 100 --batch 16 -> thay vì phải sửa trực tiếp trong code.

argparse dùng để làm gì?
    Ví dụ bình thường bạn viết:
        model = "yolov8n.pt"
        epochs = 100
        batch = 16

    Muốn đổi model: model = "yolov8m.pt"
        Bạn phải mở code sửa.

    Với argparse, bạn có thể:
        python train.py --model yolov8m.pt --epochs 50

        và Python tự lấy:
            model = "yolov8m.pt"
            epochs = 50
```
**Luồng hoạt động**
```bash
Terminal
   │
   │ python train.py --model yolo.pt --epochs 100
   ▼
argparse
   │
   ├── --model → "yolo.pt"
   └── --epochs → 100
   │
   ▼
Python program
```
# ArgumentParser (class dùng để tạo một bộ phân tích command-line arguments)
**Syn**
```bash
argparse.ArgumentParser(    
    prog=None,    
    usage=None,    
    description=None,    
    epilog=None,    
    parents=[],   
    formatter_class=argparse.HelpFormatter,    
    prefix_chars="-",    
    fromfile_prefix_chars=None,    
    argument_default=None,    
    conflict_handler="error",    
    add_help=True,    
    allow_abbrev=True
)

- Input:
    + description=str: dùng để mô tả chức năng của chương trình. Nội dung này thường xuất hiện khi người dùng chạy chương trình với --help.
```
**Ex**
```python
import argparse

cli = argparse.ArgumentParser(    
    description="Clean email thread -> Text ML & PostgreSQL"
)
cli.add_argument("--input", help="Path to input file")
args = cli.parse_args()
print(args.input)

# Bạn chạy chương trình trong terminal:
# python clean_email.py --help


# Kết quả có thể hiển thị:
# usage: clean_email.py [-h] [--input INPUT]

# Clean email thread -> Text ML & PostgreSQL

# options:
#   -h, --help     show this help message and exit
#   --input INPUT  Path to input file


# Nếu chạy:
# python clean_email.py --input emails.jsonl


# Thì:
# args.input



# sẽ có giá trị:
# emails.jsonl
```
## .add_argument() (dùng để nói cho chương trình biết command-line của chương trình nhận những tham số nào kiểu gì mặc định là gì bắt buộc hay không)
**Syn**
```bash
parser.add_argument(
    "--name",
    type=str,,
    action="store_true",
    default="unknown",
    required=True,
    help="Tên người dùng"
)

- Input:
    + type      : kiểu dữ liệu
    + default   : giá trị mặc định
    + required  : có bắt buộc hay không
    + help      : mô tả argument. Dùng để giải thích argument khi chạy
    + choices=list  : giới hạn giá trị được phép
    + action    : thay đổi cách argument hoạt động
        - store_true
    + metavar   : metavar chủ yếu để đổi cách hiển thị trong --help.
```
## .parse_args()
### .name
**Ex**
```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--name, default="Thang")

args = parser.parse_args()

print(args.name) # Thang
```