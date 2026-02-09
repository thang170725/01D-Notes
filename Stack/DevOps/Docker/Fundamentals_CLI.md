- [docker run](#docker-run)
- [docker ps](#docker-ps)
- [docker logs web](#docker-logs-web)
- [docker exec -it web bash](#docker-exec--it-web-bash)
---
# docker run
**Syn**
```bash
docker run [options] IMAGE [command]

- options:
    + -d    : mặc định container chiếm terminal.
    + -p    : mở cổng
```
**Ex**
```bash
docker run -it ubuntu bash (bạn sẽ thấy prompt bị đổi thành kiểu: root@c2a17d31f42f:/#)
 
- docker run → tạo container mới và chạy
- -it → interactive + gắn terminal
- ubuntu → tên image (Docker tự tải nếu máy bạn chưa có)
- bash → lệnh chạy khi container khởi độngcker run -it ubuntu bash
```
**Ex**
```bash
docker run -d -p 8080:80 nginx
```
# docker ps
**Syn**
```bash
1. docker ps    # container đang chạy
2. docker ps -a # tất cả container
```
# docker logs web
# docker exec -it web bash
docker stop web
docker rm web
docker rm -f web
