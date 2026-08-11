- [Argparse Introduction (dùng để nhận tham số từ command line/terminal khi chạy chương trình)](#argparse-introduction-dùng-để-nhận-tham-số-từ-command-lineterminal-khi-chạy-chương-trình)
- [ArgumentParser (class dùng để tạo một bộ phân tích command-line arguments)](#argumentparser-class-dùng-để-tạo-một-bộ-phân-tích-command-line-arguments)
  - [.add\_argument() (Nó dùng để khai báo một argument mà chương trình chấp nhận)](#add_argument-nó-dùng-để-khai-báo-một-argument-mà-chương-trình-chấp-nhận)
  - [.parse\_args()](#parse_args)
---
# Argparse Introduction (dùng để nhận tham số từ command line/terminal khi chạy chương trình)
```bash
argparse là standard library của Python. 
    Bạn chỉ cần: import argparse 
    Không cần: pip install argparse

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
parser = argparse.ArgumentParser() # Sau đó bạn định nghĩa các argument mà chương trình cho phép nhận
```
## .add_argument() (Nó dùng để khai báo một argument mà chương trình chấp nhận)
## .parse_args()
**Ex**
```python
import argparse

parser = argparse.ArgumentParser()

parser.add_argument("--name")

args = parser.parse_args()

print(args.name)

# python main.py --name Thang
# Kết quả: Thang
```