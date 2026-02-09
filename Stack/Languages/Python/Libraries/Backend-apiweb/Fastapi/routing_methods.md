- [FastAPI() \& add\_middleware](#fastapi--add_middleware)
- [get \& post \& .put()](#get--post--put)
  - [@router.post()](#routerpost)
  - [lấy data Json từ client](#lấy-data-json-từ-client)
  - [lấy data Json từ client](#lấy-data-json-từ-client-1)
- [APIRouter() \& .include\_router() \& create\_app()](#apirouter--include_router--create_app)
---
# FastAPI() & add_middleware
# get & post & .put()
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
# APIRouter() & .include_router() & create_app()
```bash
- APIRouter
    + Thay vì viết tất cả API trong main.py, ta nhóm lại để code gọn, Dễ mở rộng, Chuẩn kiến trúc (layered / clean).
    + from fastapi import APIRouter
- .include_router() : Gắn router vào app
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
