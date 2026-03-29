# Reset khóa kiểu int tự tăng về 1
```sql
ALTER TABLE ten_bang AUTO_INCREMENT = 1;

- Bảng phải trống
- Nếu vẫn còn record có id = 10 → AUTO_INCREMENT sẽ không về 1
```