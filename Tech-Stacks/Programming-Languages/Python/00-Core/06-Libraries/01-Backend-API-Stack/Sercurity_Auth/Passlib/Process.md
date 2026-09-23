# context
## CryptContext
**Ex: Tạo một CryptContext**
```python
pwd_context = CryptContext(
    schemes=["bcrypt"],
    deprecated="auto"
)

# schemes=["bcrypt"]: sử dụng thuật toán bcrypt để hash password.
# deprecated="auto": tự động đánh dấu các thuật toán cũ là deprecated khi bạn có nhiều scheme.
```
### .hash() (hash)
**Syn**
```bash
pwd_context.hash(password)
```
**Ex**
```python
from passlib.context import CryptContext

pwd_context = CryptContext(
    schemes=["bcrypt"],
    deprecated="auto"
)

password = "123456"

hashed_password = pwd_context.hash(password)

print(hashed_password) # $2b$12$LQv3c1yqBWq...

# Lần khác chạy lại:
# pwd_context.hash("123456")
# có thể ra: $2b$12$7EqJtq98hPq...
# -> Hai hash khác nhau mặc dù password giống nhau. Đây là điều bình thường vì bcrypt sử dụng salt.
```
### .verify (dùng để kiểm tra dữ liệu người dùng nhập vào có đúng với đã hash hay không)
**Syn**
```bash
pwd_context.verify(password, hashed_password)
```
**Ex**
```python
password = "123456"

hashed_password = pwd_context.hash(password)

result = pwd_context.verify(
    "123456",
    hashed_password
)

print(result) # True
```
# Practice
## Luồng thực tế khi đăng ký đăng nhập
```bash
Khi đăng ký. User nhập:
    - username: thang
    - password: 123456

Backend không nên lưu: 123456
    Mà làm: hashed_password = pwd_context.hash("123456")
```
**Ex: Ví dụ database lưu**
```bash
username          password
------------------------------------------------
thang             $2b$12$LQv3c1yqBWq...
```
**Khi login**
```bash
User nhập:
    - username: thang
    - password: 123456

Backend lấy hash từ database:
    hashed_password = "$2b$12$LQv3c1yqBWq..."
        Sau đó: pwd_context.verify( "123456", hashed_password) # True
→ Password đúng → cho đăng nhập.
```
```python
from passlib.context import CryptContext

pwd_context = CryptContext(
    schemes=["bcrypt"],
    deprecated="auto"
)

# =====================
# REGISTER
# =====================

password = "123456"

hashed_password = pwd_context.hash(password)

print("Password:", password)
print("Hash:", hashed_password)


# =====================
# LOGIN
# =====================

login_password = "123456"

if pwd_context.verify(login_password, hashed_password):
    print("Login thành công")
else:
    print("Sai password")

# Password: 123456
# Hash: $2b$12$LQv3c1yqBWq...
# Login thành công
```