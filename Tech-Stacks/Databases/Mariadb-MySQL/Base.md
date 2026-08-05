- [Directory Structure](#directory-structure)
- [Introduction](#introduction)
- [Ask](#ask)
  - [Vì sao query giống MySQL gần như 100%?](#vì-sao-query-giống-mysql-gần-như-100)
---
# Directory Structure
Mariadb/                            ```mình dùng thư mục này để xem kiến thức về Mariadb```   
├── [DB_Tables.md](DB_Tables.md)    ```mình dùng file này để thao tác với DB, Table```   
├── [Data.md](Data.md)              ```mình dùng file này đểthao tác với dữ liệu```   
├── [Practices.md](Practices.md)    ```mình dùng file này để truy vấn dữ liệu```   
└── Base.md                         ```mình dùng file này để xem kiến thức, tiện ích```    

# Introduction
```bash
- MariaDB là một hệ quản trị CSDL RIÊNG BIỆT. Không phải “chế độ” của MySQL
- MySQL ban đầu do Monty Widenius tạo. Oracle mua MySQL. Monty fork MySQL → tạo MariaDB. MariaDB = con ruột của MySQL gốc
```
# Ask
## Vì sao query giống MySQL gần như 100%?
```bash
- MariaDB giữ tương thích ngược MySQL
- Cùng SQL dialect
- Cùng protocol
- Cùng port 3306
```