- [curl (dùng để gửi request và nhận dữ liệu qua mạng)](#curl-dùng-để-gửi-request-và-nhận-dữ-liệu-qua-mạng)
---
# curl (dùng để gửi request và nhận dữ liệu qua mạng)
**Syn**
```bash

curl -X POST http://localhost:8000/login \
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"123456"}'

- Input:
    - -X POST → sử dụng HTTP method POST
    - -H → thêm HTTP header
    - -d → gửi data trong request body
```
**Ex**
```bash
curl https://example.com # Nó sẽ gửi HTTP request tới example.com và in nội dung response ra terminal
```
