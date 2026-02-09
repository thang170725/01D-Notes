Try…Except
Được dung để bắt và xử lý lỗi (exception) khi chạy chương trình, tránh chương trình bị “crash” bất ngờ.
Cú pháp:
try:
    # đoạn code có thể gây lỗi
    nguy_hiem = 10 / 0  # lỗi chia cho 0
except:
    # xử lý khi có lỗi
    print("Đã xảy ra lỗi!")
FileNotFoundError
Lỗi không tìm thấy file.
try:
    # code có thể lỗi
    f = open("file_khong_ton_tai.txt", "r")
except FileNotFoundError:
    print("Không tìm thấy file!")

ZeroDivisisionError
Lỗi chia cho không.

except ZeroDivisionError:
    print("Không được chia cho 0!")

Bắt mọi loại lỗi và xem nội dung lỗi
try:
    result = 10 / 0
except Exception as e:
    print("Có lỗi xảy ra:", e)

# raise ValueError()
```bash
Chủ động ném ra lỗi và dừng chương trình.
```
**Ex**
```python
def register(age: int):
    if age < 18:
        raise ValueError("Bạn chưa đủ 18 tuổi")
    print("Running ...")
register(15)
```# ValueError
Lỗi giá trị, chuyển đổi giá trị.
## Bắt lỗi số nhập vào phải là số nguyên
```python
while True:
    try:
        a = int(input("Nhập số nguyên: "))
        break
    except ValueError:
        print("❌ Lỗi: phải nhập số nguyên")

```- [Nhập số nguyên nhỏ hơn 5 chữ số](#nhập-số-nguyên-nhỏ-hơn-5-chữ-số)
- [Nhập vào hai số nguyên S và E, quy định S \< E và E không quá 8 chữ số.](#nhập-vào-hai-số-nguyên-s-và-e-quy-định-s--e-và-e-không-quá-8-chữ-số)

---

# Nhập số nguyên nhỏ hơn 5 chữ số
```python
while True:
    num_str = input("Nhập số nguyên 5 chữ số: ")
    try:
        num = int(num_str) # Thử ép kiểu, nếu là chữ sẽ nhảy xuống except
        if len(num_str) == 5:
            break
        else:
            print("Lỗi: Phải nhập đúng 5 chữ số!")
    except ValueError:
        # Lỗi này xảy ra khi người dùng nhập chữ (ví dụ: "abc")
        print("Lỗi: Đây không phải là số nguyên!")

print(f"Số bạn đã nhập: {num}")
```

# Nhập vào hai số nguyên S và E, quy định S < E và E không quá 8 chữ số.
```python
while True:
    SE_STR = input("S and E: ").split()
    try:
        SE = list(map(int, SE_STR))
   
        S, E = SE[0], SE[1]
        if len(str(E)) < 8 and (S < E):
            break 
    except ValueError:
        print("Error, Please again!!!")
```