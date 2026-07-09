- [Alembic Introduction (dùng để quản lý migration (di trú) cơ sở dữ liệu, thường được sử dụng cùng với SQLAlchemy)](#alembic-introduction-dùng-để-quản-lý-migration-di-trú-cơ-sở-dữ-liệu-thường-được-sử-dụng-cùng-với-sqlalchemy)
- [Installation](#installation)
---
# Alembic Introduction (dùng để quản lý migration (di trú) cơ sở dữ liệu, thường được sử dụng cùng với SQLAlchemy)
```bash
Khi bạn thay đổi cấu trúc database (thêm cột, xóa bảng, đổi kiểu dữ liệu, ...), bạn cần cập nhật database mà không làm mất dữ liệu cũ. Alembic giúp bạn:
    + Quản lý thay đổi schema database
    + Tạo bảng mới
    + Thêm / sửa / xóa cột
    + Tạo hoặc xóa index, constraint
    + Đổi tên bảng
    + Tạo migration script

Alembic sinh ra các file migration (Python script) mô tả thay đổi database.
```
# Installation 
```bash
1. pip install alembic
```