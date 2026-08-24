- [Directory Structure](#directory-structure)
- [Ask](#ask)
  - [Nên thiết quy tắc cho hệ thông như thế nào?](#nên-thiết-quy-tắc-cho-hệ-thông-như-thế-nào)
---
# Directory Structure
System-Architectures/                           ```mình dùng thư mục này để  học tư duy thiết kế hệ thống```
├── Layered-Monolith/  # mình dùng thư mục này để thiết kế theo Layered-Monolith
├── Microservies/      # mình dùng thư mục này để thiết kế hệ thống theo Microservices
└── Modular-Monolith/  # mình dùng thư mục này để thiết kế theo Modular-Monolith

# Ask
## Nên thiết quy tắc cho hệ thông như thế nào?
```bash
- Đối với độ dại 1 file (tổng lượng code + comment code không vươt quá 350 dòng) -> nếu vượt quá nên tách file
- đối với 1 folder (tổng lượng file nên giữ ở mức không vượt quá 15 file) -> nếu vượt quá 15 file thì nên tách, gom thành thư mục con
- đối với nghiệp vụ 1 file chỉ nên chứa một nghiệp vụ duy nhất (tức nó chỉ phục vụ 1 luồng xử lý)

Quy tắc đặt tên file: nên đặt file {xử lý cái gì + er}_{business}
```