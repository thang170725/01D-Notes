- [Cấu trúc đề xuất cho FastAPI](#cấu-trúc-đề-xuất-cho-fastapi)
- [Cài đặt \& run chương trình](#cài-đặt--run-chương-trình)
- [UploadFile + File() \& .read()](#uploadfile--file--read)
- [Response](#response)
---
# Cấu trúc đề xuất cho FastAPI
```bash
FastAPI/
├── 01_routing_methods.md       # Các hàm điều hướng: @app.get, @app.post, APIRouter
├── 02_params_extraction.md     # Lấy dữ liệu từ URL: Path, Query, Header, Cookie
├── 03_dependency_injection.md  # Hệ thống "tiêm" phụ thuộc: Depends, Security
├── 04_app_lifecycle.md      # Vòng đời App: lifespan, startup, shutdown, BackgroundTasks
├── 05_exception_handlers.md # Xử lý lỗi: HTTPException, exception_handler
└── 06_middlewares_cors.md   # Hàm can thiệp hệ thống: add_middleware, CORS
```
**Chi tiết cách "nét" hàm vào FastAPI:**
```bash
1. 01_routing_methods.md (Điều hướng)
    + Các hàm: FastAPI(), APIRouter(), include_router().
    + Mục đích: Cách chia nhỏ các file route và gộp chúng lại vào file main.
2. 02_params_extraction.md (Bóc tách dữ liệu)
    + Các hàm: Path(), Query(), Header(), Cookie(), File(), UploadFile().
    + Lý do: Đây là các hàm của riêng FastAPI dùng để đánh dấu xem một biến lấy từ đâu trên Request.
3. 03_dependency_injection.md (Hàm Depends)
    + Các hàm: Depends().
    + Lý do: Đây là đặc sản của FastAPI. Bạn dùng nó để gọi các hàm validate hoặc lấy DB session (nhưng logic DB nằm ở folder khác).
4. 04_app_lifecycle.md (Hành động ngầm)
    + Các hàm: BackgroundTasks(), lifespan.
    + Mục đích: Cách chạy một tác vụ sau khi đã trả về response, hoặc dọn dẹp tài nguyên khi tắt server.
5. 05_exception_handlers.md (Báo lỗi)
    + Các hàm: HTTPException(), @app.exception_handler().
    + Lý do: Cách FastAPI can thiệp vào luồng lỗi để trả về JSON chuẩn cho client.
```
# Cài đặt & run chương trình
```bash
- pip install fastapi uvicorn
- uvicorn backend.api.register:app --reload --port 3651 (để chạy chương trình)
```



# UploadFile + File() & .read()
Đại diện cho file được upload từ form-data
**Syn**
```bash
image: UploadFile = File(...)
- File(...) → bắt buộc phải có.
- UploadFile → FastAPI xử lý stream (tốt hơn bytes).
- <input type="file" name="image"> name="image" PHẢI TRÙNG với biến image.
```
**Ex**
```python
from fastapi import APIRouter, UploadFile, File, Depends
from fastapi.responses import Response
from backend.app.services.user_service import UserService

router = APIRouter(prefix="/user", tags=["User"])

def get_user_service() -> UserService:
    return UserService()

@router.post("/image-grayscale")
async def image_grayscale(
    image: UploadFile = File(...),
    service: UserService = Depends(get_user_service)
):
    image_bytes = await image.read() # bytes, Đây chính là: PNG / JPG raw bytes, Chưa decode, Chưa là numpy, Chưa là ảnh OpenCV
    result_bytes = await service.grayscale_image(image_bytes=image_bytes)

    return Response(
        content=result_bytes,
        media_type='image/png'
    )
```
# Response
- cần from fastapi.responses import Response
- Khi nào dùng Response? Khi KHÔNG trả JSON
- Bạn đang trả: bytes, ảnh PNG -> bắt buộc dùng Response