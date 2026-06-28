# Directory Structure
```bash
MongoDB/
├── 01_Concepts_Modeling.md    # Tư duy NoSQL: Document, Collection, Schema Design
├── 02_CRUD_Basic.md           # Thao tác cơ bản: Insert, Find, Update, Delete
├── 03_Query_Operators.md      # Bộ lọc nâng cao: $gt, $in, $elemMatch, $regex
├── 04_Aggregation_Pipeline.md # Xử lý dữ liệu tập trung: $match, $group, $lookup
├── 05_Indexing_Performance.md # Tối ưu hóa: Single, Compound, TTL, Text Index
└── 06_Driver_Python_Motor.md  # Kết nối với Python (PyMongo hoặc Motor cho FastAPI)
```
# Installation
```bash
1. Cài tool cần thiết
    + sudo apt update
    + sudo apt install -y curl gnupg
2. Import key MongoDB
    + curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \ sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
3. Thêm repo MongoDB
    + echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] \
https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | \
sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
4. Cài MongoDB
    + sudo apt update
    + sudo apt install -y mongodb-org
5. Khởi động & enable
    + sudo systemctl start mongod
    + sudo systemctl enable mongod
6. Kiểm tra
    + mongosh
```