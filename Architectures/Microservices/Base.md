- [Directory Structure](#directory-structure)
- [Instroduction](#instroduction)
---
# Directory Structure
```bash
Microservices/        # mình dùng thư mục này để xem hệ thống theo Microservices
├── Architecture.md   # mình dùng file này để xem cách thiết kế hệ thống theo Microservice
├── Base.md           # mình dùng file này để xem kiến thức cốt lõi và tiện ích
└── Practices.md      # mình dùng file này để xem code mẫu, bài tập, ví dụ minh họa
```
# Instroduction
```bash
- Microservice là kiến trúc, không phải chân lý.
- Nó rất mạnh khi:
    + Hệ thống rất lớn
    + Nhiều team làm song song
    + Mỗi phần scale độc lập
    + Có DevOps + CI/CD xịn
- Nhưng đổi lại:
    + Debug mệt
    + Triển khai phức tạp
    + Network latency
    + Over-engineering nếu dự án nhỏ / vừa
    -> 90% dự án ban đầu KHÔNG cần microservice
```