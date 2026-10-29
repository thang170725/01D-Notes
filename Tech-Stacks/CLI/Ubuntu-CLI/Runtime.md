- [curl (dùng để gửi request và nhận dữ liệu qua mạng)](#curl-dùng-để-gửi-request-và-nhận-dữ-liệu-qua-mạng)
  - [curl -i ... (chỉ xem HTTP status và header)](#curl--i--chỉ-xem-http-status-và-header)
  - [curl -X ... -H ... -d (gủi post request)](#curl--x---h---d-gủi-post-request)
---
# curl (dùng để gửi request và nhận dữ liệu qua mạng)
**Ex: Gửi GET request**
```bash
curl http://127.0.0.1:8000/health
# {"status":"ok"}
```
## curl -i ... (chỉ xem HTTP status và header)
**Ex**
```bash
curl -i http://127.0.0.1:8000/health
# HTTP/1.1 200 OK
# content-type: application/json

# {"status":"ok"}
```
## curl -X ... -H ... -d (gủi post request)
**Ex**
```bash
curl -X POST http://localhost:8000/login \ 
  -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"123456"}'
# -X POST → sử dụng HTTP method POST
# -H → thêm HTTP header
# -d → gửi data trong request body
```
