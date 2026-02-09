- [Directory Structure](#directory-structure)
---
# Directory Structure
```bash
Microservices/
├── 01_Communication.md       # "Nói chuyện": Cách các service gọi nhau (REST, gRPC, Message Queue)
├── 02_Data_Management.md      # "Dữ liệu": Mỗi service một DB, cách đồng bộ dữ liệu (Saga, Event)
├── 03_API_Gateway.md         # "Cửa ngõ": Một điểm đón khách duy nhất (Auth, Routing, Rate Limit)
├── 04_Reliability.md         # "Chống sập": Ngắt mạch (Circuit Breaker), Retry, chịu lỗi
├── 05_Observability.md       # "Giám sát": Xem log tập trung, theo vết lỗi (Tracing) giữa các service
└── 06_Python_NodeJS_InterOp.md # "Thực hành": Code mẫu Python gọi NodeJS và ngược lại
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