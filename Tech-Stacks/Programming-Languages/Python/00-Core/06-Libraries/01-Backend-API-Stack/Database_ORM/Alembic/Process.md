- [Command (lệnh alembic CLI)](#command-lệnh-alembic-cli)
  - [alembic revision --autogenerate -m ...](#alembic-revision---autogenerate--m-)
  - [alembic upgrade head](#alembic-upgrade-head)
  - [alembic current (Kiểm tra database hiện tại đang ở migration/version nào)](#alembic-current-kiểm-tra-database-hiện-tại-đang-ở-migrationversion-nào)
  - [alembic\_version](#alembic_version)
  - [alembic\_version](#alembic_version-1)
- [op (operation object)](#op-operation-object)
  - [.create\_table()](#create_table)
  - [.drop\_table()](#drop_table)
  - [.add\_column()](#add_column)
  - [drop\_column()](#drop_column)
  - [alter\_column()](#alter_column)
  - [.create\_foreign\_key()](#create_foreign_key)
  - [.drop\_constraint()](#drop_constraint)
  - [.create\_index()](#create_index)
  - [.drop\_index()](#drop_index)
  - [.create\_unique\_constraint()](#create_unique_constraint)
  - [.execute()](#execute)
- [Practices](#practices)
  - [Các set up Alembic](#các-set-up-alembic)
  - [Migration khác Model ở điểm nào?](#migration-khác-model-ở-điểm-nào)
- [sửa model](#sửa-model)
---
# Command (lệnh alembic CLI)
## alembic revision --autogenerate -m ...
**Ex**
```bash
Giả sử ban đầu trong python bạn có:
    class Document(Base):
        __tablename__ = "documents"

        id = Column(Integer, primary_key=True)
        OCR_DOC_ID = Column(String)

Bạn sửa:
    class Document(Base):
        __tablename__ = "documents"

        id = Column(Integer, primary_key=True)
        OCR_DOC_ID = Column(String)
        status = Column(String)  # thêm
-> bây giờ có sự khác biệt
SQLAlchemy Model:
    documents
    ├── id
    ├── OCR_DOC_ID
    └── status       ← CÓ
nhưng db hiện tại vẫn:
PostgreSQL:
    documents
    ├── id
    └── OCR_DOC_ID

Bạn chạy: alembic revision --autogenerate -m "add status to documents"
    Alembic sẽ so sánh đại khái:
        SQLAlchemy Model
               │
               │
               │ so sánh
               ↓
        Database hiện tại

    Nó phát hiện:
        Model:
            documents
            ├── id
            ├── OCR_DOC_ID
            └── status
        Database:
            documents
            ├── id
            └── OCR_DOC_ID
    => phát hiện: status cần được thêm

Alembic tạo migration:
    def upgrade():
        op.add_column(
            "documents",
            sa.Column("status", sa.String())
        )
-> Đây chính là migration.
```
## alembic upgrade head
**Ex**
```bash
Giả sử database hiện tại đang ở: 001_add_status

Nhưng code mới đã có migration: 002_add_created_at

Bạn chạy: alembic upgrade head

Alembic nhìn vào lịch sử:
    001_add_status
           ↓
    002_add_created_at   ← HEAD

    và chạy migration còn thiếu:
        001
         ↓
        002

Database sau đó trở thành:
    documents
    ├── id
    ├── OCR_DOC_ID
    ├── status
    └── created_at
```
## alembic current (Kiểm tra database hiện tại đang ở migration/version nào)
```bash
Nó không thay đổi database, chỉ đọc trạng thái hiện tại.
```
**Ex**
```bash
alembic current
# 3ee781b36280 (head)

# Điều này có nghĩa:
# Database hiện tại
#    ↓
# 3ee781b36280
#    ↓
# đang là HEAD
# Tức là database của bạn đã chạy đến migration mới nhất.
```
Liên hệ với alembic upgrade head

Hai lệnh này khác nhau:

alembic current

→ Hỏi: "Database đang ở đâu?"

alembic upgrade head

→ Ra lệnh: "Đưa database lên phiên bản mới nhất."

Ví dụ:

Migration history:


A
↓
B
↓
C (head)

Database hiện tại đang ở:

A

Bạn chạy:

alembic current

→

A

Sau đó:

alembic upgrade head

Alembic chạy:

A → B → C

Chạy lại:

alembic current

→

C (head)
Trong trường hợp của bạn

Bạn vừa chạy:

alembic upgrade head

và thấy:

Running upgrade de4d21dd12ae -> 3ee781b36280

Bây giờ chạy:

alembic current

nếu thấy:

3ee781b36280 (head)

thì có nghĩa:

Database của bạn đã ở đúng migration mới nhất.

Một cách nhớ rất đơn giản
alembic current
        ↓
"Đang ở đâu?"

alembic history
        ↓
"Có những migration nào?"

alembic upgrade head
        ↓
"Đi đến mới nhất."

alembic downgrade -1
        ↓
"Lùi lại 1 migration."
stamp trong Alembic có thể hiểu đơn giản là “đánh dấu database đang ở migration nào”.

Vì vậy:

alembic stamp head

có nghĩa là:

Đánh dấu database hiện tại đang ở migration mới nhất (head), nhưng KHÔNG chạy các migration.

So sánh với upgrade head

Đây là điểm rất quan trọng:

alembic upgrade head

→ Thực sự chạy migration.

Ví dụ migration của bạn có:

def upgrade():
    op.create_index(
        "ix_ocr_document_ocr_doc_id",
        "ocr_document",
        ["ocr_doc_id"]
    )

Khi chạy:

alembic upgrade head

Alembic sẽ thực hiện:

Database
   ↓
tạo index
   ↓
cập nhật alembic_version

Còn:

alembic stamp head

→ Không thực hiện upgrade().

Nó chỉ cập nhật bảng:

alembic_version

thành revision mới nhất.

Ví dụ hiện tại:

alembic_version
----------------
de4d21dd12ae

chạy:

alembic stamp head

thì thành:

alembic_version
----------------
3ee781b36280

nhưng index/table/column mà migration 3ee781b36280 tạo ra sẽ không tự nhiên được tạo.

Khi nào dùng stamp?

Trường hợp phổ biến nhất:

Database đã có schema đúng rồi, nhưng Alembic chưa biết database đang ở revision nào.

Ví dụ bạn có database:

PostgreSQL
├── users
├── documents
├── ocr_document
└── index ix_ocr_document_ocr_doc_id   ← đã tồn tại

Nhưng Alembic lại nghĩ:

database đang ở de4d21dd12ae

Trong khi thực tế schema đã tương ứng với:

3ee781b36280

Bạn có thể:

alembic stamp 3ee781b36280

hoặc:

alembic stamp head

để nói với Alembic:

"Schema hiện tại đã tương ứng với revision này rồi, đừng chạy lại migration."

Nhớ 3 lệnh này
Lệnh	Ý nghĩa
alembic upgrade head	Chạy migration đến mới nhất
alembic downgrade -1	Lùi 1 migration
alembic stamp head	Đánh dấu đang ở mới nhất, không chạy migration

Nói ngắn gọn:

upgrade = làm thật
stamp = chỉ nói cho Alembic biết trạng thái

Với trường hợp bạn vừa chạy alembic upgrade head và thấy Running upgrade de4d21dd12ae -> 3ee781b36280, thì không cần stamp head nữa — Alembic đã tự cập nhật alembic_version rồi.
# op (operation object)
## .create_table()
```bash
dùng để tạo bảng
```
**Ex**
```python
from alembic import op
import sqlalchemy as sa

op.create_table(
    "table_name",
    sa.Column("id", sa.Integer, primary_key=True),
    sa.Column("name", sa.String(100), nullable=False),
    sa.Column("created_at", sa.DateTime),
)
```
## .drop_table()
```bash
Để xóa bảng.
```
**Syn**
```bash
op.drop_table("table_name")
```
## .add_column()
```bash
Để thêm cột.
```
**Syn**
```bash
op.add_column(
    "table_name",
    sa.Column("age", sa.Integer, nullable=True)
)
```
## drop_column()
```bash
Xóa cột
```
**Syn**
```bash
op.drop_column("table_name", "age")
```
## alter_column()
```bash
Để sửa cột.
```
**Ex**
```python
op.alter_column(
    "users",
    "email",
    existing_type=sa.String(255),
    nullable=False
)
```
## .create_foreign_key()
```bash
Tạo khóa ngoài
```
**Syn**
```bash
op.create_foreign_key(
    "fk_name",
    "child_table",
    "parent_table",
    ["child_column"],
    ["parent_column"],
    ondelete="CASCADE"
)
```
## .drop_constraint()
```bash
Xóa khóa ngoài
```
**Syn**
```bash
op.create_foreign_key(
    "fk_name",
    "child_table",
    "parent_table",
    ["child_column"],
    ["parent_column"],
    ondelete="CASCADE"
)
```
## .create_index()
```bash
Tạo index.
```
**Syn**
```bash
op.create_index(
    "ix_name",
    "table_name",
    ["column_name"],
    unique=False
)
```
## .drop_index()
```bash
Xóa index
```
**Syn**
```bash
op.drop_index("ix_name", table_name="table_name")
```
## .create_unique_constraint()
```bash
Tạo Unique Constraint
```
**Syn**
```bash
op.create_unique_constraint(
    "uq_name",
    "table_name",
    ["column_name"]
)
```
## .execute()
```bash
Thực thi raw SQL
```
**Syn**
```bash
op.execute("UPDATE users SET active = 1")
```
# Practices
## Các set up Alembic
```bash
alembic init migrations
    + Tạo các file setup migrations
    + alembic.ini → cấu hình database
    + env.py → nơi Alembic kết nối với project của bạn
    + versions/ → nơi chứa các file migration
3. alembic.ini
    + tìm dòng sqlalchemy.url = driver://user:pass@localhost/dbname và thay đường dẫn đến db
4. env.py
    + Tìm dòng: target_metadata = None
    + Sửa thành:
        from your_model_file import Base        
        target_metadata = Base.metadata
    + Ví dụ nếu model bạn nằm ở models.py:
        from models import Base
        target_metadata = Base.metadata
5. alembic stamp head
    + Nó chỉ đánh dấu: "DB này đang ở version mới nhất".
6. alembic revision -m "add email to users"
    + Tạo migration mới
    + Nó sẽ tạo file trong: migrations/versions/xxxxxxxx_add_email_to_users.py
7. Viết nội dung migration
    + Mở file đó và chỉnh:
        from alembic import op
        import sqlalchemy as sa

        def upgrade():
            op.add_column(
                "users",
                sa.Column("email", sa.String(50), nullable=True)
            )

        def downgrade():
            op.drop_column("users", "email")
8. alembic upgrade head --sql
    + test
9. alembic upgrade head
    + Chạy migration
    + Lúc này nó sẽ chỉ chạy:
    + ALTER TABLE users ADD COLUMN email VARCHAR(50);
    + Không đụng bảng khác.
```
## Migration khác Model ở điểm nào?
```bash
Model nói: Database nên trông như thế nào.
    Ví dụ: status = Column(String)

Migration nói: Để đi từ database cũ sang database mới, hãy làm gì.
    Ví dụ:
        op.add_column(
            "documents",
            sa.Column("status", sa.String())
        )

    Migration có lịch sử
        Giả sử database ban đầu:
            v1
            documents
            ├── id
            └── OCR_DOC_ID

        Bạn thêm status:
            v2
            documents
            ├── id
            ├── OCR_DOC_ID
            └── status

    Migration:
        v1
         ↓
        migration 001
         ↓
        v2

Sau đó bạn lại thêm: created_at
    Database:
        v3
        documents
        ├── id
        ├── OCR_DOC_ID
        ├── status
        └── created_at

    Lịch sử:
        v1
         ↓
        001_add_status
         ↓
        002_add_created_at
         ↓
        v3
-> Đây là lý do migration giống Git commit.
```
trường hợp tôi có db rồi nhưng muốn dùng alembic sau đó thì phải làm như nào , nếu chạy init rồi chay alembic revision --autogenerate -m thì nó sé ra file .py mà bên trong sẽ kiểu toàn create, những thật ra là có bảng, có db, có dữ liệu sẵn từ trước rồi tôi chỉ muốn alembic bắt đầu quản lý thay đổi từ lúc này thôi
Đúng, trường hợp của bạn là “đưa một database đã tồn tại vào quản lý bằng Alembic”. Đây là case rất phổ biến.

Điểm quan trọng là:

Bạn không muốn Alembic tạo lại schema hiện tại. Bạn chỉ muốn lấy schema hiện tại làm mốc ban đầu, rồi từ đó Alembic quản lý các thay đổi về sau.

Cách làm đúng

Giả sử hiện tại DB của bạn đã có:

my_database
├── users
├── orders
├── products
└── ...

và tất cả bảng + dữ liệu đã tồn tại.

1. Khởi tạo Alembic
alembic init alembic

Sau đó cấu hình sqlalchemy.url trong alembic.ini hoặc env.py.

2. Tạo migration baseline

Bạn có thể chạy:

alembic revision --autogenerate -m "baseline"

Alembic sẽ nhìn vào DB hiện tại và models của bạn.

Nếu DB và model khớp nhau, thường file migration sẽ gần như:

def upgrade():
    pass


def downgrade():
    pass

Hoặc có thể Alembic vẫn sinh ra một số create_table, add_column... nếu model và DB chưa khớp hoàn toàn.

Không được chạy file này lên DB hiện tại nếu nó chứa các lệnh tạo những thứ đã tồn tại.

3. Quan trọng nhất: stamp

Sau khi bạn kiểm tra rằng:

"DB hiện tại chính là trạng thái mà tôi muốn coi là baseline."

thì chạy:

alembic stamp head

Alembic sẽ ghi revision hiện tại vào bảng:

alembic_version

Nhưng không chạy upgrade().

Ví dụ:

DB hiện tại
│
├── users          ← đã có
├── products       ← đã có
├── orders         ← đã có
└── data           ← đã có
       │
       ▼
alembic stamp head
       │
       ▼
alembic_version = abc123

Dữ liệu không bị ảnh hưởng.

Nhưng có một điểm cần chú ý

Cách bạn nói:

alembic revision --autogenerate -m "baseline"

rồi:

alembic stamp head

có thể làm được, nhưng tôi khuyên bạn hiểu rõ một vấn đề:

Migration baseline không nhất thiết phải chứa create_table

Nếu DB hiện tại đã tồn tại và bạn muốn:

"Từ thời điểm này Alembic bắt đầu quản lý"

thì baseline nên đại diện cho trạng thái hiện tại, chứ không phải migration dùng để tạo DB từ số 0.

Có 2 hướng.

Cách tôi khuyên dùng
Bước 1 — DB đã tồn tại
DB
├── users
├── orders
├── products
└── ...
Bước 2 — Model SQLAlchemy phải phản ánh đúng DB

Ví dụ:

class User(Base):
    __tablename__ = "users"


    id = Column(Integer, primary_key=True)
    name = Column(String)

...

Bước 3 — Generate thử
alembic revision --autogenerate -m "baseline"

Kiểm tra file sinh ra.

Nếu thấy:

def upgrade():
    op.create_table(...)
    op.create_table(...)

thì đừng chạy upgrade.

Bạn cần xem tại sao Alembic nghĩ những bảng đó chưa tồn tại.

Có thể do:

model chưa khai báo đầy đủ
Alembic chưa import tất cả model
target_metadata chưa đúng
tên bảng khác
schema khác
index/constraint khác
column khác
Bước 4 — Khi DB và model đã khớp

Bạn có thể tạo baseline migration.

Ví dụ revision:

a1b2c3d4_baseline.py

Sau đó:

alembic stamp a1b2c3d4

hoặc nếu đó là revision cuối:

alembic stamp head

Kết quả:

Database
   │
   ├── users
   ├── orders
   ├── products
   └── data
        │
        ▼
   Alembic baseline
        │
        ▼
   alembic_version
   = a1b2c3d4
Sau đó phát triển bình thường

Ví dụ hôm nay bạn muốn thêm:

users
    ↓
+ email

Bạn sửa model:

class User(Base):
    __tablename__ = "users"


    id = Column(Integer, primary_key=True)
    name = Column(String)
    email = Column(String)

Sau đó:

alembic revision --autogenerate -m "add email to users"

Alembic sẽ sinh:

def upgrade():
    op.add_column(
        "users",
        sa.Column("email", sa.String(), nullable=True)
    )




def downgrade():
    op.drop_column("users", "email")

Lúc này:

alembic upgrade head

mới là lúc Alembic thực sự thay đổi DB.

Hình dung toàn bộ quá trình
              DATABASE ĐÃ TỒN TẠI
                      │
                      │
              users, orders,...
                      │
                      ▼
              alembic init
                      │
                      ▼
          cấu hình SQLAlchemy models
                      │
                      ▼
       revision --autogenerate "baseline"
                      │
                      ▼
             kiểm tra migration
                      │
             ┌────────┴────────┐
             │                 │
          không khớp          khớp
             │                 │
        sửa models             │
             │                 │
             └────────┬────────┘
                      ▼
                stamp baseline
                      │
                      ▼
          Alembic bắt đầu quản lý
                      │
                      ▼
          ┌──────────────────────┐
          │ Thay đổi model       │
          │       ↓              │
          │ revision --autogen   │
          │       ↓              │
          │ upgrade head         │
          └──────────────────────┘
Một câu cực kỳ quan trọng

stamp không có nghĩa là "Alembic tạo baseline từ database".

Nó chỉ có nghĩa:

"Alembic, hãy coi database này đang ở revision X."

Vì vậy, nếu bạn đang có DB production với rất nhiều dữ liệu, cách tiếp cận an toàn là:

DB hiện tại → đảm bảo models khớp → tạo baseline → stamp baseline → từ đó trở đi dùng revision --autogenerate + upgrade.

Nếu bạn muốn, tôi có thể chỉ cho bạn 
một quy trình cụ thể từ A-Z với FastAPI + SQLAlchemy + Alembic, bao gồm cả trường hợp revision --autogenerate sinh ra hàng loạt create_table dù bảng đã tồn tại, và cách xử lý env.py/target_metadata cho đúng.

Đúng — đây chính là chỗ dễ nhầm nhất khi đưa DB có sẵn vào Alembic.

Nếu bạn chạy:

alembic revision --autogenerate -m "baseline"

và file sinh ra kiểu:

def upgrade():
    op.create_table(
        "users",
        ...
    )


    op.create_table(
        "orders",
        ...
    )

trong khi users, orders đã tồn tại trong DB, thì đừng chạy alembic upgrade head.

Cách xử lý

Bạn cần phân biệt 2 việc:

autogenerate
    ↓
Alembic so sánh MODEL ↔ DATABASE
    ↓
sinh ra migration

Còn:

upgrade
    ↓
thực thi migration
    ↓
thay đổi DATABASE

Trong trường hợp của bạn, migration sinh ra create_table có nghĩa là:

Alembic đang cho rằng những table đó chưa tồn tại trong database.

1. Trước tiên: tìm nguyên nhân tại sao Alembic không nhận ra bảng

Ví dụ DB có:

users
orders
products

nhưng migration lại sinh:

def upgrade():
    op.create_table("users", ...)
    op.create_table("orders", ...)
    op.create_table("products", ...)

Thường nguyên nhân nằm ở env.py.

Bạn cần kiểm tra:

target_metadata = Base.metadata

Ví dụ:

from app.models.base import Base


target_metadata = Base.metadata

Quan trọng: tất cả model phải được import trước khi lấy Base.metadata.

Ví dụ bạn có:

app/
├── models/
│   ├── user.py
│   ├── order.py
│   └── product.py
└── models/base.py

Nếu env.py chỉ:

from app.models.base import Base


target_metadata = Base.metadata

nhưng chưa import:

User
Order
Product

thì Base.metadata có thể không chứa các table đó.

2. Nhưng trường hợp của bạn còn có một vấn đề khác

Giả sử bạn kiểm tra và chắc chắn:

DB:
users
orders
products


Model:
users
orders
products

vậy mà Alembic vẫn sinh:

op.create_table("users")

thì cần kiểm tra Alembic đang kết nối tới đúng database chưa.

Đây là lỗi rất hay gặp.

Ví dụ bạn tưởng đang kết nối:

my_database

nhưng Alembic thực tế đang kết nối:

my_database_dev

hoặc:

localhost:5432

thay vì:

192.xxx.xxx.xxx:5432

Khi đó:

DB bạn kiểm tra:
users        ✓
orders       ✓


DB Alembic đang kiểm tra:
users        ✗
orders       ✗

→ tất nhiên Alembic sẽ sinh create_table.

3. Kiểm tra nhanh

Bạn có thể chạy:

alembic current

và:

alembic heads

Nhưng hai lệnh này chủ yếu kiểm tra revision.

Bạn cần xác nhận connection string mà Alembic đang sử dụng.

Ví dụ trong env.py:

url = config.get_main_option("sqlalchemy.url")
print("ALEMBIC DATABASE:", url)

rồi:

alembic revision --autogenerate -m "baseline"

xem nó đang connect tới đâu.

4. Nếu xác nhận DB + model đều đúng thì làm gì?

Nếu bạn chắc chắn:

DB hiện tại:
    users ✓
    orders ✓
    products ✓


Model:
    users ✓
    orders ✓
    products ✓


Alembic:
    đúng database ✓
    đúng metadata ✓

nhưng migration baseline vẫn sinh:

op.create_table(...)

thì không nên chạy migration đó.

Bạn có thể xóa revision vừa tạo:

alembic/versions/
└── abc123_baseline.py   ← xóa

Sau đó tạo một baseline migration rỗng:

alembic revision -m "baseline"

Nó sẽ có:

def upgrade():
    pass




def downgrade():
    pass

Sau đó:

alembic stamp head

Kết quả:

DB hiện tại
     │
     │ không thay đổi
     ▼
┌─────────────────┐
│ users           │
│ orders          │
│ products        │
│ data...         │
└─────────────────┘
        │
        │ stamp
        ▼
alembic_version
      = baseline

Từ migration tiếp theo:

alembic revision --autogenerate -m "add email"

Alembic sẽ bắt đầu quản lý thay đổi.

5. Có một cách rất quan trọng khác

Nếu migration baseline của bạn đang chứa create_table, nhưng bạn muốn giữ file migration đó để sau này một database mới hoàn toàn có thể tạo được toàn bộ schema, thì đừng xóa nó.

Ví dụ baseline:

def upgrade():
    op.create_table("users", ...)
    op.create_table("orders", ...)

File này rất có giá trị nếu bạn muốn:

Database mới
     ↓
alembic upgrade head
     ↓
users
orders
products
...

Nhưng với DB cũ, bạn không chạy nó.

Bạn chỉ:

alembic stamp <baseline_revision>

Nói cách khác, cùng một migration có thể được dùng theo hai tình huống:

DB MỚI
   │
   ▼
alembic upgrade head
   │
   ▼
create_table
create_table
create_table




DB CŨ
   │
   ▼
đã có table rồi
   │
   ▼
alembic stamp <baseline>
   │
   ▼
không chạy create_table

Đây mới là cách rất hay để xử lý database legacy.

Và đây là điểm tôi muốn bạn nhớ

Nếu bạn có:

def upgrade():
    op.create_table("users")

thì:

alembic stamp head

không chạy create_table.

Nó chỉ nói:

"Alembic, hãy coi DB này đã ở revision này."

Do đó bạn không cần sửa upgrade() thành pass chỉ để stamp.

Quy trình tôi khuyên cho case của bạn
DB cũ đã có dữ liệu
        │
        ▼
alembic init
        │
        ▼
cấu hình đúng DB
        │
        ▼
đảm bảo Base.metadata chứa tất cả models
        │
        ▼
alembic revision --autogenerate -m "baseline"
        │
        ▼
migration có create_table
        │
        ├──── DB CŨ ────→ KHÔNG upgrade
        │                   │
        │                   ▼
        │              alembic stamp <revision>
        │
        └──── DB MỚI ───→ alembic upgrade head

Sau đó từ ngày hôm đó:

# sửa model
alembic revision --autogenerate -m "add xxx"
alembic upgrade head

là quy trình bình thường.

Một lưu ý cuối: nếu mục tiêu của bạn là vừa có DB cũ tiếp tục chạy, vừa muốn sau này có thể alembic upgrade head trên DB mới từ số 0, thì baseline có create_table là hoàn toàn bình thường. Đừng biến nó thành pass một cách máy móc. Chỉ cần DB cũ stamp revision đó, còn DB mới thì upgrade