- [Create](#create)
  - [jwt.encode](#jwtencode)
---
# Create
## jwt.encode()
```bash
- Dùng để tạo (ký) JWT token từ:
    + Payload (dữ liệu)
    + Secret key
    + Thuật toán mã hóa
- Thường dùng trong xác thực (login).
- Thư viện hay dùng: PyJWT
```
**Syn**
```bash
jwt.encode(payload, key, algorithm="HS256")

- payload   : dict chứa dữ liệu (user_id, exp…)
- key       : secret key để ký
- algorithm : thuật toán ký (thường là "HS256")
```
**Ex**
```python
from jose import jwt
from datetime import datetime, timedelta, timezone

SECRET_KEY = "mysecret"
ALGORITHM = "HS256"
ACCESS_TOKEN_EXPIRE_MINUTES = 60

expire = datetime.now(timezone.utc) + timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)

data = {
    "sub": "user123",
    "exp": expire
}

token = jwt.encode(data, SECRET_KEY, algorithm=ALGORITHM)

print(token) # eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ1c2VyMTIzIiwiZXhwIjoxNzcwOTkxNDE2fQ.ynFDrGXqpffkG3fucbG6pIhxy-lfMxWuaDoNzHaFlWU
```