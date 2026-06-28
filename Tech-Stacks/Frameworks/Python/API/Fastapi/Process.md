- [App Configuration](#app-configuration)
  - [FastAPI()](#fastapi)
    - [.include\_router()](#include_router)
      - [APIRouter()](#apirouter)
    - [.add\_middleware()](#add_middleware)
      - [CORSMiddleware](#corsmiddleware)
    - [.mount()](#mount)
- [Routing (HTTP Methods)](#routing-http-methods)
- [.get() \& .post() \& .put()](#get--post--put)
  - [@router.post()](#routerpost)
  - [lấy data Json từ client](#lấy-data-json-từ-client)
  - [lấy data Json từ client](#lấy-data-json-từ-client-1)
- [Authentication](#authentication)
  - [OAuth2PasswordBearer()](#oauth2passwordbearer)
- [Dependency Injection](#dependency-injection)
  - [Depends](#depends)
- [File (Nhóm xử lý file)](#file-nhóm-xử-lý-file)
  - [Create (Nhóm khởi tạo)](#create-nhóm-khởi-tạo)
  - [UploadFile \& File()](#uploadfile--file)
  - [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
    - [.filename](#filename)
  - [.content\_type](#content_type)
  - [.file](#file)
  - [await file.read()](#await-fileread)
- [Response](#response)
  - [HTTPException](#httpexception)
---
# App Configuration
```bash
- Nhóm này chứa các thành phần dùng để khởi tạo và cấu hình ứng dụng FastAPI, bao gồm tạo app, chia router, thêm middleware và mount các ứng dụng hoặc static service khác.
- Mục đích chính:
    + Tạo app FastAPI
    + Tổ chức cấu trúc project
    + cấu hình middleware
    + mount app hoặc static files
```
## FastAPI() 
```bash
- Dùng để tạo một ứng dụng web API. 
- Đây là đối tượng trung tâm của toàn bộ ứng dụng – nơi bạn đăng ký route, middleware, dependency, cấu hình OpenAPI, v.v.
- FastAPI được xây dựng dựa trên:
    + FastAPI
    + Starlette (ASGI framework nền tảng)
    + Pydantic (validate dữ liệu)
```
**Syn**
```bash
from fastapi import FastAPI

FastAPI(
    title="FastAPI",
    description=None,
    version="0.1.0",
    openapi_url="/openapi.json",
    docs_url="/docs",
    redoc_url="/redoc",
    debug=False,
    middleware=None,
    routes=None
)

- title         : tiêu đề hiển thị trong Swagger
- description   : mô tả API
- version       : phiên bản API
- docs_url      : Đổi đường dẫn Swagger UI
- redoc_url     : đổi đường dẫn ReDoc
- openapi_url   : đường dẫn file OpenAPI JSON
- debug         : 
```
### .include_router() 
```bash
Gắn router vào app.
```
**Syn**
```bash
app.include_router(routes_user.router) # routes_user là file bên trong có biến router
```
#### APIRouter()
```bash
- Thay vì viết tất cả API trong main.py, ta nhóm lại để code gọn, Dễ mở rộng, Chuẩn kiến trúc (layered / clean).
- from fastapi import APIRouter
```
**Syn: APIRouter**
```bash
router = APIRouter(prefix="/user", tags=["User"])

- prefix="/user": @router.get("/data-left") -> URL thực tế /user/data-left
    + Tránh lặp /user ở từng route
    + Dễ versioning (/api/v1/user)
- tags=["User"]: Chỉ dùng cho Swagger UI /docs
    + Nó giúp: nhóm API, dễ đọc, không ảnh hưởng runtime
```
### .add_middleware()
```bash
Dùng để thêm middleware vào ứng dụng FastAPI
```
**Syn**
```bash
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Domain được phép gọi API
    allow_credentials=True,
    allow_methods=["*"],  # GET, POST, PUT...
    allow_headers=["*"],
)

- allow_origins     : Domain được phép
- allow_methods	    : HTTP methods được phép
- allow_headers	    : Header được phép
- allow_credentials : Cho phép gửi cookie
```
#### CORSMiddleware
```bash
- CORSMiddleware là middleware dùng để cho phép frontend (khác domain/port) gọi API backend.
- Ví dụ:
    + Frontend: http://localhost:3000
    + Backend: http://localhost:8000
- Nếu không bật CORS → trình duyệt sẽ chặn request.
```
### .mount()
```bash
gắn (mount) một ứng dụng ASGI khác vào một đường dẫn cụ thể.
```
**Syn**
```bash
app.mount(
    path: str,
    app: ASGIApp,
    name: Optional[str] = None
)

- path	: URL prefix
- app	: ASGI app (StaticFiles, sub FastAPI app, etc)
- name	: Tên để reverse URL
```
**Ex**
```bash
project/
│
├── main.py
└── images/
    └── cat.jpg
```
```python
from fastapi import FastAPI
from fastapi.staticfiles import StaticFiles
import os

app = FastAPI() # -> Đây là ASGI app 

images_path = os.path.join(os.getcwd(), "images") # /home/thang/project/images

# MỌI request bắt đầu bằng /images
# sẽ KHÔNG đi vào router FastAPI nữa
# mà chuyển sang StaticFiles xử lý.
app.mount(
    "/images",                         # URL prefix
    StaticFiles(directory=images_path),# Thư mục thật trên ổ cứng
    name="images"                      # Tên để reverse URL (ít dùng)
)
```
# Routing (HTTP Methods) 
```bash
- Nhóm này định nghĩa các endpoint API và cách server phản hồi khi client gửi request thông qua các HTTP method như GET, POST, PUT.
- Mục đích chính:
    + tạo endpoint API
    + xử lý request từ client
    + map URL → function xử lý
```
# .get() & .post() & .put()
```bash
- put   : Cập nhật dữ liệu đã tồn tại
- post  : Tạo mới
```
## @router.post()
**Syn**
```bash
@router.post("", response_model=Token)

- response_model    : Nói với FastAPI rằng: “API này khi trả response thì phải có shape giống Token”
- Token             : Là Pydantic model
```
## lấy data Json từ client
```bash
backend/
├── app.py   
├── api    
├    └── register.py
```
**app.py**
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

from backend.api import register 

def create_app() -> FastAPI:
    app = FastAPI(
        title="Backend API",
        version="1.0.0", 
    )

    # CORS
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],
        allow_methods=["*"],
        allow_headers=["*"],
    )

    # Routers
    app.include_router(register.router)

    return app

app = create_app()
```
**register.py**
```python
from backend.schemas.user import UserSchema
from fastapi import APIRouter

router = APIRouter(prefix="/register", tags=["Register"])

@router.post('')
async def fetch_data(user: UserSchema):
    print(user)

    return {
        'message': "user received",
        'data': user
    }
```
**Ex1: put**
**User trong database**
```json
{
  "id": 1,
  "username": "thang",
  "email": "thang@gmail.com",
  "age": 20
}
```
```python
@router.put("/users/{user_id}", response_model=UserSchema)
def update_user(
    user_id: int,
    payload: UserUpdateSchema,
    db: Session = Depends(get_db)
):
    user = db.query(User).filter(User.id == user_id).first()

    if not user:
        raise HTTPException(status_code=404, detail="User not found")

    user.username = payload.username
    user.email = payload.email
    user.age = payload.age

    db.commit()
    db.refresh(user)

    return user
```
**Payload gửi từ frontend**
```json
{
  "username": "thang123",
  "email": "thang123@gmail.com",
  "age": 22
}

// Toàn bộ user bị thay đổi theo payload
```
## lấy data Json từ client 
```python
from backend.schemas.user import UserSchema
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.post('/register')
async def fetch_data(user: UserSchema):
    print(user)

    return {
        'message': "user received",
        'data': user
    }
```

- [Depends](#depends)
---
# Authentication
```bash
- Nhóm này xử lý xác thực người dùng, đảm bảo chỉ những client hợp lệ mới truy cập được API.
- Mục đích chính:
    + xác thực token
    + bảo vệ endpoint
    + tích hợp OAuth2
```
## OAuth2PasswordBearer()
```bash
- Lấy Bearer Token từ HTTP Header
- Bắt buộc endpoint phải có token
- Trả về token dạng string
```
**Ex**
```python
from fastapi import FastAPI, Depends
from fastapi.security import OAuth2PasswordBearer
from fastapi.testclient import TestClient

app = FastAPI()

# Khai báo OAuth2
oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/login")

# Endpoint test
@app.get("/profile")
def get_profile(token: str = Depends(oauth2_scheme)):
    print("TOKEN NHẬN ĐƯỢC:", token)
    return {
        "received_token": token
    }

# Tạo client test
client = TestClient(app)

# Fake request có header Authorization
response = client.get(
    "/profile",
    headers={"Authorization": "Bearer fake_token_123"}
)

print("RESPONSE JSON:", response.json())

# TOKEN NHẬN ĐƯỢC: fake_token_123
# RESPONSE JSON: {'received_token': 'fake_token_123'}
```
# Dependency Injection
```bash
- Nhóm này cho phép tái sử dụng logic chung (database, auth, config...) bằng cơ chế dependency injection của FastAPI.
- Mục đích chính:
    + chia sẻ logic giữa các endpoint
    + inject service hoặc database
    + xử lý security dependency
```
## Depends
```bash
- Depends = cơ chế “nhờ FastAPI làm hộ việc chuẩn bị thứ mình cần”
- Bạn không tự tạo nữa, FastAPI tiêm (inject) vào cho bạn.
```
**Ex1: quán cà phê**
**không dùng Depends**
```bash
“Tôi muốn cà phê, đây là tiền điện, tiền nước, máy pha, nhân viên…”
```
**Cách dùng Depends**
```bash
“Cho tôi 1 ly cà phê”
- Quán tự lo:
    + Điện
    + Máy
    + Nhân viên
    + Nước
```
**Ex2**
**Không dùng Depends**
```python
@app.get("/items")
def get_items():
    db = SessionLocal()  # tự tạo
    items = db.query(Item).all()
    db.close()
    return items

# Vấn đề: Lặp code, Dễ quên close(), Khó test
```
**Dùng Depends**
```python
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()

@app.get("/items")
def get_items(db: Session = Depends(get_db)):
    return db.query(Item).all()

# FastAPI làm thay bạn:
# Gọi get_db()
# Lấy db
# Inject vào function
# Xong request → tự đóng DB
```
# File (Nhóm xử lý file)
## Create (Nhóm khởi tạo)
## UploadFile & File()
**Syn**
```bash
from fastapi import FastAPI, File, UploadFile

app = FastAPI()

@app.post("/upload")
async def upload_file(file: UploadFile = File(...)):
    return {"filename": file.filename}

```
## Display (Nhóm cung cấp thông tin)
### .filename
```bash
Tên file
```
## .content_type
```bash
kiểu file
```
## .file
```bash
file object thật
```
## await file.read()
```bash
Đọc nội dung
```
# Response
## HTTPException
```bash
- dùng để:
    + Chủ động trả lỗi HTTP cho client
    + Dừng xử lý request ngay lập tức
    + Trả về status code + message rõ ràng
- Các lỗi:
    + 400 : Client gửi sai dữ liệu
    + 401 : Chưa đăng nhập / token sai
    + 404 : Không tìm thấy user
    + 401 : Sai mật khẩu
    + 400 : Thiếu dữ liệu
    + 500 : Lỗi server
- Thay vì để app crash, bạn dùng HTTPException để trả lỗi đúng chuẩn REST
```
**Syn**
```bash
from fastapi import HTTPException

raise HTTPException(
    status_code=404,
    detail="User not found"
)
```
**Ex**
```python
from fastapi import FastAPI, HTTPException

app = FastAPI()

fake_users = {"thang": "123"}

@app.get("/users/{username}")
async def get_user(username: str):
    if username not in fake_users:
        raise HTTPException(
            status_code=404,
            detail="User not found"
        )
    return {"username": username}
```