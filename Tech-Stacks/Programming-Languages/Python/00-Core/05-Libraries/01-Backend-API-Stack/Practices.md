# Demo workflow quy trình kết nối csdl bằng sqlalchemy và quản lý miggrations bằng alembic
```bash
my_project/
│
├── src/
│   ├── __init__.py
│   ├── database.py      # Cấu hình kết nối SQLAlchemy (Engine, Session)
│   └── models.py        # Định nghĩa các bảng dữ liệu (SQLAlchemy Models)
│
├── main.py              # File chạy ứng dụng chính
├── requirements.txt     # Các thư viện cần thiết
└── (Sau khi init Alembic, các thư mục migrations sẽ tự động sinh ra ở đây)
```
**Step 1: Cài đặt các thư viện cần thiết (requirements.txt)**
```bash
sqlalchemy>=2.0.0
alembic>=1.13.0
psycopg2-binary>=2.9.0  # Hoặc asyncpg nếu dùng async, pymysql nếu dùng MySQL
```
2. Thiết lập SQLAlchemy (Kết nối & Models ban đầu)
Bước 1: Cấu hình kết nối (src/database.py)
Sử dụng cú pháp SQLAlchemy 2.0 mới với DeclarativeBase.

Python


from sqlalchemy import create_engine
from sqlalchemy.orm import DeclarativeBase, sessionmaker

# Thay thế bằng URL DB thực tế của bạn (PostgreSQL, MySQL, SQLite...)
DATABASE_URL = "postgresql://user:password@localhost:5432/my_database"

engine = create_engine(DATABASE_URL, echo=True)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)

# Base class để các models kế thừa
class Base(DeclarativeBase):
    pass

# Dependency để lấy DB Session (tiện cho FastAPI hoặc script)
def get_db():
    db = SessionLocal()
    try:
        yield db
    finally:
        db.close()
Bước 2: Định nghĩa Model ban đầu (src/models.py)
Tạo một bảng User đơn giản làm mẫu.

Python


from sqlalchemy import String
from sqlalchemy.orm import Mapped, mapped_column
from src.database import Base

class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(primary_key=True, autoincrement=True)
    username: Mapped[str] = mapped_column(String(50), unique=True, nullable=False)
    email: Mapped[str] = mapped_column(String(100), unique=True, nullable=False)
3. Khởi tạo và Cấu hình Alembic (Chỉ làm 1 lần)
Thay vì dùng Base.metadata.create_all(engine) khiến việc sửa đổi bảng sau này gặp khó khăn, ta sẽ dùng Alembic để quản lý database từ đầu.

Bước 1: Khởi tạo Alembic trong thư mục gốc
Mở terminal tại thư mục my_project/ và chạy:

Bash


alembic init alembic
Thư mục alembic/ và file cấu hình alembic.ini sẽ xuất hiện.

Bước 2: Liên kết Alembic với Database và Models
Để Alembic tự động nhận diện các thay đổi trong file models.py (tính năng Autogenerate), bạn cần chỉnh sửa 2 file:

Trong file alembic.ini: Tìm dòng sqlalchemy.url và cập nhật kết nối tới DB của bạn:

Ini, TOML


sqlalchemy.url = postgresql://user:password@localhost:5432/my_database
Trong file alembic/env.py: Tìm đến đoạn cấu hình target_metadata (khoảng dòng 20-25) và sửa đổi để import Base từ dự án của bạn:

Python


# 1. Import Base metadata từ project
from src.database import Base
import src.models  # Ép alembic load các model để nhận diện bảng

# 2. Gán target_metadata bằng metadata của Base
target_metadata = Base.metadata
4. Quy trình Tạo và Chạy Migration ban đầu (First Migration)
Bây giờ ta sẽ tạo bảng users lần đầu tiên trên database thông qua Alembic.

1
Tạo file Migration tự động
Chạy lệnh terminal
Chạy lệnh sau để Alembic so sánh models.py với Database hiện tại (đang trống) và sinh file code migration:

Bash


alembic revision --autogenerate -m "create users table"
Một file mới sẽ được sinh ra trong thư mục alembic/versions/ (ví dụ: 1a2b3c4d5e6f_create_users_table.py).

2
Kiểm tra file Migration
Đọc lại file vừa sinh ra
Mở file phiên bản vừa sinh ra trong alembic/versions/ để kiểm tra xem hàm upgrade() và downgrade() đã đúng ý bạn chưa trước khi áp dụng vào DB.

3
Áp dụng Migration vào Database
Chạy lệnh terminal
Đẩy cấu trúc bảng lên Database thật:

Bash


alembic upgrade head
Lúc này trên DB sẽ xuất hiện bảng users và một bảng alembic_version để lưu dấu vết phiên bản hiện tại.


5. Quy trình Sửa đổi Bảng biểu & Dữ liệu (Quy trình lặp lại hàng ngày)
Mỗi khi bạn muốn thêm cột, sửa cột, xóa cột, hoặc tạo bảng mới, bạn sẽ lặp lại quy trình dưới đây.

Giả sử bài toán: Bạn cần thêm cột phone_number vào bảng users và tạo thêm một bảng mới tên là Post.

Bước 1: Cập nhật thay đổi trong src/models.py
Sửa đổi file models để phản ánh cấu trúc mới:

Python


from typing import List
from sqlalchemy import String, ForeignKey, Text
from sqlalchemy.orm import Mapped, mapped_column, relationship
from src.database import Base

class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(primary_key=True, autoincrement=True)
    username: Mapped[str] = mapped_column(String(50), unique=True, nullable=False)
    email: Mapped[str] = mapped_column(String(100), unique=True, nullable=False)
    
    # 1. CỘT MỚI THÊM
    phone_number: Mapped[str | None] = mapped_column(String(20), nullable=True) 
    
    # Relationship (không ảnh hưởng trực tiếp cấu trúc bảng DB nhưng cần cho SQLAlchemy)
    posts: Mapped[List["Post"]] = relationship(back_populates="author")

# 2. BẢNG MỚI THÊM
class Post(Base):
    __tablename__ = "posts"

    id: Mapped[int] = mapped_column(primary_key=True, autoincrement=True)
    title: Mapped[str] = mapped_column(String(200), nullable=False)
    content: Mapped[str] = mapped_column(Text, nullable=False)
    user_id: Mapped[int] = mapped_column(ForeignKey("users.id"), nullable=False)

    author: Mapped["User"] = relationship(back_populates="posts")
Bước 2: Tạo và chạy Migration mới
Chạy lệnh tự động phát hiện thay đổi:

Bash


alembic revision --autogenerate -m "add phone_number and create posts table"
Alembic sẽ tự quét file models.py, phát hiện bạn đã thêm trường phone_number và tạo class Post, sau đó tự viết code tạo bảng/thêm cột vào file script mới trong thư mục versions/.

Áp dụng thay đổi lên DB:

Bash


alembic upgrade head
6. Các lệnh hữu ích khi làm việc thực tế
Xem trạng thái hiện tại của DB (Đang ở migration nào):

Bash


alembic current
Quay xe (Rollback) lại 1 version ngay trước đó khi xảy ra lỗi:

Bash


alembic downgrade -1
Xem lịch sử các bản migration đã tạo:

Bash


alembic history --verbose
Lưu ý quan trọng: Không bao giờ sửa trực tiếp cấu trúc bảng bằng các công cụ như DBeaver, PGAdmin,... khi đã dùng Alembic. Mọi thay đổi về schema (bảng biểu) bắt buộc phải đi từ sửa code trong models.py -> chạy alembic revision -> chạy alembic upgrade.