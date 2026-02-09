- [Depends](#depends)
---
# Depends
```bash
- Depends = cơ chế “nhờ FastAPI làm hộ việc chuẩn bị thứ mình cần”
- Bạn không tự tạo nữa, FastAPI tiêm (inject) vào cho bạn.
```
**Ex: quán cà phê**
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