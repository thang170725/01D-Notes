- [Pathlib Introduction (Dùng để thao tác với file và thư mục theo cách hiện đại hơn os.path. code sẽ dễ đọc hơn os)](#pathlib-introduction-dùng-để-thao-tác-với-file-và-thư-mục-theo-cách-hiện-đại-hơn-ospath-code-sẽ-dễ-đọc-hơn-os)
- [Ask](#ask)
  - [pathlib có nhanh bằng os không?](#pathlib-có-nhanh-bằng-os-không)
---
# Pathlib Introduction (Dùng để thao tác với file và thư mục theo cách hiện đại hơn os.path. code sẽ dễ đọc hơn os)
```bash
pathlib là thư viện chuẩn của Python (Standard Library) không cần tải. 
```
# Ask
## pathlib có nhanh bằng os không?
```bash
Nếu bạn hỏi về tốc độ, thì câu trả lời ngắn là: 
    pathlib không nhanh hơn os đáng kể, và trong đa số chương trình bạn sẽ không cảm nhận được sự khác biệt.

Điểm khác nhau chủ yếu là API và cách viết, không phải hiệu năng.
    - Nếu xét performance
        Có thể hình dung:
            Python code
                ↓
            pathlib / os
                ↓
            system call
                ↓
            filesystem
                ↓
            SSD / HDD
        -> Chi phí lớn thường nằm ở:
            - filesystem
            - disk I/O
            - network filesystem
            - chứ không phải:
                + pathlib
                + os
```