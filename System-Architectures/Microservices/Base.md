- [Directory Structure](#directory-structure)
- [Instroduction](#instroduction)
---
[<<Back](../Base.md)
# Directory Structure
Microservices/        # mình dùng thư mục này để xem hệ thống theo Microservices
├── [Architecture](Architecture.md)     ```mình dùng file này để xem cách thiết kế hệ thống theo Microservice```  
└── Practices.md      # mình dùng file này để xem code mẫu, bài tập, ví dụ minh họa

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