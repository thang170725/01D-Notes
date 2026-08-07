# Cấu trúc chuẩn xử lý ảnh và post lên frontent (fastapi)
**backend/app/core/test.py**
Nơi để xử lý tính toán nặng.
```python
import cv2
import numpy as np

class ProcessImage:
    def __init__(self):
        ...
    
    def grayscale(self, image: np.ndarray) -> np.ndarray:
        gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

        return gray
```
**backend/app/services/user_service.py**
Nơi để làm cầu nối cho xử lý ảnh và chuẩn hóa ảnh đưa lên frontend
```python
from backend.app.core.test import ProcessImage
import cv2
import numpy as np

class UserService:
    def __init__(self) -> None:
        self.processor = ProcessImage()

    async def grayscale_image(self,
        image_bytes: bytes    
    ) -> bytes:
        np_arr = np.frombuffer(image_bytes, np.uint8)
        image = cv2.imdecode(np_arr, cv2.IMREAD_COLOR)

        if image is None:
            raise ValueError("Image is not invalid")
        
        result = self.processor.grayscale(image=image)

        _, buffer = cv2.imencode(".png", result)

        return buffer.tobytes()
```
**backend/app/routers/user.py**
Bộ định cho main tuyến xây dựng API cho backend
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
    image_bytes = await image.read()
    result_bytes = await service.grayscale_image(image_bytes=image_bytes)

    return Response(
        content=result_bytes,
        media_type='image/png'
    )
```

**backend/app/main.py**
Nơi tiếp xúc trực tiếp với frontend.
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

from backend.app.routers import user

def create_app() -> FastAPI:
    app = FastAPI(
        title="Backend API",
        version="1.0.0",
        docs_url="/docs",
        redoc_url="/redoc",
    )

    # CORS
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],
        allow_methods=["*"],
        allow_headers=["*"],
    )

    # Routers
    app.include_router(user.router)

    return app

app = create_app()
```

# Cấu trúc chuẩn xử lý video và post lên frontend (fastapi)
**backend/app/core/test.py**
```python
import cv2
import numpy as np

class ProcessImage:
    def grayscale(self, frame: np.ndarray) -> np.ndarray:
        return cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
```
**backend/app/services/user_service.py**
```python
import cv2
from backend.app.core.test import ProcessImage

class UserService:
    def __init__(self) -> None:
        self.processor = ProcessImage()

    def process_video(self, input_path: str, output_path: str):
        cap = cv2.VideoCapture(input_path)

        width  = int(cap.get(cv2.CAP_PROP_FRAME_WIDTH))
        height = int(cap.get(cv2.CAP_PROP_FRAME_HEIGHT))
        fps    = cap.get(cv2.CAP_PROP_FPS)

        fourcc = cv2.VideoWriter_fourcc(*'mp4v')
        out = cv2.VideoWriter(
            output_path,
            fourcc,
            fps,
            (width, height),
            isColor=False
        )

        while cap.isOpened():
            ret, frame = cap.read()
            if not ret:
                break

            gray = self.processor.grayscale(frame)
            out.write(gray)

        cap.release()
        out.release()
```
**backend/app/routers/user.py**
```python
from fastapi import APIRouter, UploadFile, File, Depends
from fastapi.responses import FileResponse
from backend.app.services.user_service import UserService

router = APIRouter(prefix="/user", tags=["User"])

def get_user_service() -> UserService:
    return UserService()

@router.post("/video-process")
async def video_process(
    video: UploadFile = File(...),
    service: UserService = Depends(get_user_service)
):
    input_path = "input.mp4"
    output_path = "output.mp4"

    with open(input_path, "wb") as f:
        f.write(await video.read())

    service.process_video(input_path, output_path)

    return FileResponse(
        output_path,
        media_type="video/mp4",
        filename="result.mp4"
    )
```
**backend/app/main.py**
```python
from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

from backend.app.routers import user

def create_app() -> FastAPI:
    app = FastAPI(
        title="Backend API",
        version="1.0.0",
        docs_url="/docs",
        redoc_url="/redoc",
    )

    # CORS
    app.add_middleware(
        CORSMiddleware,
        allow_origins=["*"],
        allow_methods=["*"],
        allow_headers=["*"],
    )

    # Routers
    app.include_router(user.router)

    return app

app = create_app()
```