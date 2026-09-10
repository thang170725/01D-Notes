+ [<<Back](../Base.md)
- [Directory Structure](#directory-structure)
- [Clean Code (Code không chỉ cần chạy đúng mà phải dễ đọc, dễ hiểu, dễ thay đổi và khó làm hỏng)](#clean-code-code-không-chỉ-cần-chạy-đúng-mà-phải-dễ-đọc-dễ-hiểu-dễ-thay-đổi-và-khó-làm-hỏng)
  - [Đừng viết code thừa](#đừng-viết-code-thừa)
  - [Comment không phải lúc nào cũng tốt](#comment-không-phải-lúc-nào-cũng-tốt)
  - [Đừng để function có quá nhiều tham số](#đừng-để-function-có-quá-nhiều-tham-số)
- [do something](#do-something)
- [Ask](#ask)
  - [Tại sao phải viết code?](#tại-sao-phải-viết-code)
  - [Tại sao phải học lập trình?](#tại-sao-phải-học-lập-trình)
  - [Có phải ai cũng cần học lập trình?](#có-phải-ai-cũng-cần-học-lập-trình)
---
# Directory Structure
Programming-Languages/                  ```mình dùng thư mục này để xem kiến thức về ngôn ngữ lập trình```  
├── Javascript  # mình dùng thư mục này để xem kiến thức về Javascript  
├── Html        # mình dùng thư mục này để xem kiến thức về Html       
├── Css         # mình dùng thư mục này để xem kiến thức về Css  
├── Java        # mình dùng thư mục này để xem kiến thức về Java  
├── Java        # mình dùng thư mục này để xem kiến thức về Java  
└── [Python](Python/Base.md)            ```mình dùng thư mục này để xem kiến thức về Python```  

# Clean Code (Code không chỉ cần chạy đúng mà phải dễ đọc, dễ hiểu, dễ thay đổi và khó làm hỏng)
**Tài liệu về clean code**
[A Handbook of Agile Software Sraftsmanship](https://drive.google.com/file/d/1anGq4rROh7DAF-c35-k7a3cizXHu9F6L/view)
**Tên biến, hàm, class phải nói lên ý nghĩa -> tên tốt giúp code tự giải thích chính nó**
**không nên**
```bash
d = 5

def process(data):
    ...
```
**nên**
```bash
days_until_expiration = 5

def create_invoice(order):
    ...
```
**Function nên nhỏ (đây là một trong những ý quan trọng nhất của clean code**
**không nên**
```bash
def process_order(order):
    # validate
    # calculate price
    # apply discount
    # create invoice
    # send email
    # save database
    # logging
    # ...
```
**nên**
```bash
def process_order(order):
    validate_order(order)
    price = calculate_price(order)
    invoice = create_invoice(order, price)
    save_invoice(invoice)
    send_invoice_email(invoice)
# Mỗi function nên có một trách nhiệm rõ ràng.
```
**Mỗi function nên làm một việc**
## Đừng viết code thừa
**Nếu có**
```bash
if user is not None:
    if user.is_active:
        if user.has_permission:
            ...
# đừng ngay lập tức làm code phức tạp hơn chỉ để "clean".
# Mục tiêu không phải: Code càng ít dòng càng tốt.
# Mà là: Code càng dễ hiểu càng tốt.
# Đôi khi 10 dòng rõ ràng tốt hơn 3 dòng "ảo thuật".
```
## Comment không phải lúc nào cũng tốt
```bash
Nhiều người nghĩ: Code khó hiểu → thêm comment.

Clean Code có quan điểm khá mạnh:
    Nếu có thể viết code rõ ràng hơn thì ưu tiên sửa code thay vì giải thích bằng comment.
```
**Ví dụ:**
```python
# Check if user is old enough to buy alcohol
if user.age >= 18:
```
**Có thể tốt hơn**
```python
if user.is_adult(): # Code tự nói lên ý nghĩa.
```
## Đừng để function có quá nhiều tham số
**Không tốt**
```python
create_user(
    name,
    age,
    email,
    address,
    phone,
    role,
    department,
    ...
)
```
**Có thể dùng object**
```python
class User:
    name
    age
    email
    address
    phone
    role

create_user(user) # Code sẽ dễ đọc hơn.
```
Đừng lặp code — DRY

DRY = Don't Repeat Yourself.

Ví dụ:

price1 = price * 0.9
price2 = price * 0.9
price3 = price * 0.9

Nếu logic giảm giá thay đổi:

10% → 15%

bạn phải sửa nhiều chỗ.

Tách:

def apply_discount(price):
    return price * 0.9

Sau đó:

apply_discount(price1)
apply_discount(price2)
apply_discount(price3)
8. Nhưng đừng "DRY quá mức"

Đây là nuance rất quan trọng.

Không phải cứ code giống nhau là phải gom lại.

Ví dụ hôm nay:

calculate_user_price()
calculate_product_price()

có vẻ giống nhau.

Bạn gom thành:

calculate_price()

Nhưng 2 logic này thực chất có thể thay đổi độc lập trong tương lai.

Khi đó abstraction sớm có thể làm code khó hiểu hơn.

Vì vậy:

Đừng chỉ nhìn code giống nhau; hãy nhìn xem chúng có cùng ý nghĩa và cùng lý do để thay đổi hay không.

9. Error handling cũng là một phần của thiết kế

Đừng để code:

try:
    ...
except:
    pass

Đây là rất nguy hiểm.

Nên xử lý rõ:

try:
    user = get_user(user_id)
except UserNotFoundError:
    return None

Tức là:

Biết mình đang bắt lỗi gì và tại sao.

10. Exception tốt hơn return "magic value"

Ví dụ:

def get_user(id):
    return -1

-1 nghĩa là gì?

Người đọc phải đoán.

Có thể:

def get_user(id):
    raise UserNotFoundError()

Sau đó:

try:
    user = get_user(123)
except UserNotFoundError:
    ...

Ý nghĩa rõ hơn rất nhiều.

11. Class cũng phải có trách nhiệm rõ ràng

Không nên có:

class UserManager:
    # database
    # email
    # payment
    # authentication
    # logging
    # report

Class này trở thành một God Object.

Tách:

UserRepository
UserService
EmailService
PaymentService
AuthService

Ví dụ:

UserService
    ↓
UserRepository
12. Cohesion và Coupling

Đây là hai khái niệm cực kỳ quan trọng khi code lớn.

High Cohesion

Một class/function nên chứa những thứ liên quan chặt chẽ với nhau.

UserService
 ├── create_user
 ├── update_user
 └── delete_user

→ hợp lý.

Nhưng:

UserService
 ├── create_user
 ├── send_email
 ├── calculate_tax
 ├── resize_image
 └── generate_pdf

→ cohesion thấp.

Low Coupling

Các module không nên phụ thuộc quá chặt vào nhau.

Ví dụ:

OrderService
     │
     └── phụ thuộc trực tiếp MySQL

sau này muốn chuyển PostgreSQL sẽ khó.

Clean Architecture thường hướng tới:

OrderService
     │
     ▼
Repository Interface
     │
     ├── MySQLRepository
     └── PostgreSQLRepository
13. Code nên dễ thay đổi

Đây có lẽ là một trong những mục tiêu lớn nhất của Clean Code.

Hôm nay:

Payment → Stripe

Ngày mai:

Payment → PayPal

Nếu code viết tốt:

payment_service.pay(order)

bên dưới có thể thay implementation.

Thay vì code khắp nơi:

stripe.PaymentIntent.create(...)
14. Đừng phụ thuộc implementation nếu không cần

Ví dụ:

class OrderService:
    def __init__(self):
        self.db = MySQLDatabase()

OrderService bị khóa vào MySQL.

Có thể thiết kế:

class OrderService:
    def __init__(self, repository):
        self.repository = repository

Sau đó:

repository = MySQLOrderRepository()

service = OrderService(repository)

Đây là Dependency Injection.

15. Test rất quan trọng

Clean Code không chỉ là format code.

Code tốt phải dễ test.

Ví dụ:

def calculate_discount(price, percentage):
    return price * (1 - percentage)

Rất dễ test:

assert calculate_discount(100, 0.1) == 90

Trong khi một function 300 dòng:

def process_everything():
    ...

rất khó test.

Một dấu hiệu:

Nếu một function cực kỳ khó viết unit test, có khả năng design của nó đang có vấn đề.

16. Refactoring là công việc liên tục

Clean Code không có nghĩa:

"Viết một lần và code sẽ clean mãi."

Thực tế:

Write
 ↓
Run
 ↓
Test
 ↓
Refactor
 ↓
Improve
 ↓
Repeat

Ví dụ ban đầu:

def process(data):
    ...

Sau vài lần refactor:

def process_order(order):
    validate_order(order)
    calculate_total(order)
    save_order(order)

Code ngày càng rõ.

17. Code smell

Một phần tư duy quan trọng của Clean Code là biết nhận ra code smell.

Ví dụ thấy:

if ...
if ...
if ...
if ...
if ...

hoặc:

def function(a, b, c, d, e, f, g):

hoặc:

class SomethingManagerEverything:

hoặc:

try:
    ...
except:
    pass

hoặc:

# do something
x = x + 1

thì nên dừng lại và hỏi:

"Có vấn đề về design ở đây không?"

18. Clean Code không đồng nghĩa với "code đẹp"

Đây là điều mình muốn bạn nhớ nhất.

Clean Code không phải:

✓ format đẹp
✓ tên biến đẹp
✓ ít dòng

Mà là:

Code
 │
 ├── Dễ đọc
 ├── Dễ hiểu
 ├── Dễ test
 ├── Dễ sửa
 ├── Dễ mở rộng
 └── Khó vô tình phá vỡ
19. Nếu chỉ nhớ 10 điều

Nếu bạn không muốn đọc cả cuốn sách, hãy nhớ 10 điều này:

1. Đặt tên có ý nghĩa
        ↓
2. Function nhỏ
        ↓
3. Một function một trách nhiệm
        ↓
4. Class có trách nhiệm rõ ràng
        ↓
5. Không lặp code vô lý
        ↓
6. Không abstraction quá sớm
        ↓
7. Error handling rõ ràng
        ↓
8. Giảm coupling
        ↓
9. Viết code dễ test
        ↓
10. Refactor liên tục
20. Và có một câu mình nghĩ rất đáng nhớ

Khi bạn code:

Đừng chỉ nghĩ "máy có chạy được không?"

Hãy nghĩ thêm:

"3 tháng nữa, một developer khác đọc đoạn code này có hiểu nó không?"

Đó gần như là tinh thần của Clean Code.

Đặc biệt với những project backend/microservice kiểu bạn đang tìm hiểu, Clean Code sẽ bắt đầu quan trọng hơn rất nhiều khi code chuyển từ:

1 file
   ↓
5 file
   ↓
20 file
   ↓
100 file
   ↓
nhiều service

Ở quy mô nhỏ, code bẩn vẫn chạy được. Ở quy mô lớn, code bẩn làm tốc độ phát triển giảm cực mạnh và bug tăng lên.
# Ask
## Tại sao phải viết code?
```bash
Code là cách chúng ta ra lệnh cho máy tính thực hiện công việc.
    Nếu không có code, máy tính chỉ là một thiết bị không biết phải làm gì. -> để ra lệnh cho máy làm việc ta cần diễn đạt bằng ngôn ngữ lập trình

Ví dụ:
    - Muốn máy tính cộng hai số → viết code.
    - Muốn tạo website → viết code.
    - Muốn AI nhận diện chữ ký, khuôn mặt, biển số xe → viết code.
    - Muốn tự động xử lý hàng nghìn file Excel hay PDF → viết code.
```
## Tại sao phải học lập trình?
```bash
Có nhiều lý do.
    1. Để giải quyết vấn đề: Lập trình giúp biến một công việc thủ công thành tự động.
        Ví dụ:
            Trước đây: Mở 1000 file PDF -> Cắt từng ảnh -> Lưu từng file -> Mất vài ngày
            lập trình: viết code -> Có thể hoàn thành trong vài phút.

    2. Để tạo ra sản phẩm 
        Hầu hết phần mềm đều được tạo bằng lập trình:
            - Facebook
            - YouTube
            - TikTok
            - Zalo
            - Shopee
            - ChatGPT
        => Đằng sau mỗi ứng dụng đều là hàng triệu dòng code.
    
    3. Để làm việc với AI
        AI không tự xuất hiện. Để sử dụng AI hiệu quả, bạn thường cần biết lập trình để:
            - huấn luyện mô hình,
            - xử lý dữ liệu,
            - xây dựng ứng dụng,
            - triển khai mô hình lên máy chủ.

    4. Để tăng năng suất
        Ví dụ: 
            Một người nhập dữ liệu mất: 5 phút cho một file.
                1000 file: khoảng 83 giờ.

            Nếu viết chương trình: chỉ mất vài phút hoặc vài chục phút. -> Đó là lý do doanh nghiệp rất coi trọng tự động hóa.

    5. Để rèn tư duy
        Học lập trình không chỉ là học cú pháp.

        Bạn học cách:
            - chia nhỏ vấn đề,
            - suy nghĩ logic,
            - tìm nguyên nhân khi có lỗi,
            - thiết kế lời giải hiệu quả.

Những kỹ năng này hữu ích ngay cả ngoài lĩnh vực CNTT.

Kết luận: Lý do cốt lõi để học lập trình không phải là để "biết viết code", mà là để:
    - Giải quyết vấn đề bằng máy tính.
    - Tự động hóa những công việc lặp đi lặp lại.
    - Xây dựng phần mềm, website và ứng dụng AI.
    - Biến ý tưởng thành sản phẩm mà người khác có thể sử dụng.

Nói ngắn gọn: lập trình là cách giao tiếp với máy tính để khiến nó làm những gì bạn muốn. Khi bạn biết lập trình, bạn không chỉ sử dụng phần mềm của người khác mà còn có thể tự tạo ra phần mềm của chính mình.
```
## Có phải ai cũng cần học lập trình?
```bash
Không. Nếu công việc của bạn không liên quan đến công nghệ thì có thể không cần.

Nhưng nếu bạn làm trong các lĩnh vực như:
    - AI
    - Khoa học dữ liệu
    - Phát triển phần mềm
    - Tự động hóa
    - Phân tích dữ liệu
    - An ninh mạng
    - Robot
    - IoT
=> thì lập trình gần như là kỹ năng nền tảng.

Một ví dụ dễ hiểu:
    Hãy tưởng tượng:
        - Máy tính là một người công nhân rất chăm chỉ.
        - Code là bản hướng dẫn công việc.

    Nếu bạn nói: "Làm giúp tôi."

    Người công nhân sẽ hỏi: "Làm cái gì?"

    Nhưng nếu bạn đưa hướng dẫn từng bước:
        - Mở thư mục.
        - Đọc file PDF.
        - Chuyển thành ảnh.
        - Chạy AI nhận diện.
        - Lưu kết quả.
    => thì máy tính có thể làm chính xác hàng nghìn lần mà không mệt.
```