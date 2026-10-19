- [.sh (shell script - một file chứa nhiều lệnh terminal được viết sẵn để chạy tự động)](#sh-shell-script---một-file-chứa-nhiều-lệnh-terminal-được-viết-sẵn-để-chạy-tự-động)
  - [Practices](#practices)
  - [Dúngh để setup chạy frontend và bacekend trên cùng một terminal](#dúngh-để-setup-chạy-frontend-và-bacekend-trên-cùng-một-terminal)
  - [Dấu \& trong shell là gì](#dấu--trong-shell-là-gì)
- [wait (Đợi tất cả các tiến trình chạy nền kết thúc rồi mới kết thúc script)](#wait-đợi-tất-cả-các-tiến-trình-chạy-nền-kết-thúc-rồi-mới-kết-thúc-script)
---
# .sh (shell script - một file chứa nhiều lệnh terminal được viết sẵn để chạy tự động)
**Ex: Chạy một file python ở test.sh**
```sh
# (.venv) thang@PhatToNhuLai:~/workspace/test/python-test$ chmod +x test.sh (bước 1 cấp quyền để chạy)
echo "Run..."
python test.py
# (.venv) thang@PhatToNhuLai:~/workspace/test/python-test$ ./test.sh
# Run...
```
## Practices
## Dúngh để setup chạy frontend và bacekend trên cùng một terminal
**Ví dụ cấu trúc dự án**
```bash
my-project/
├── backend/
│   └── pom.xml
├── frontend/
│   └── package.json
└── start.sh
```
*start.sh*
```sh
#!/bin/bash

echo "Starting backend..."
cd backend
mvn spring-boot:run &

BACKEND_PID=$!

cd ../frontend

echo "Starting frontend..."
npm run dev &

FRONTEND_PID=$!

echo "Backend PID: $BACKEND_PID"
echo "Frontend PID: $FRONTEND_PID"

wait
```
*Cấp quyền*
```sh
chmod +x start.sh
```
*Chạy*
```sh
./start.sh
```
## Dấu & trong shell là gì
```bash
Chạy lệnh ở background (chạy nền), để terminal không phải chờ lệnh đó kết thúc.
    Đây là lý do tại sao bạn có thể chạy nhiều chương trình cùng lúc.
```
**Không có &**
```bash
mvn spring-boot:run
npm run dev

Shell sẽ chạy:

mvn spring-boot:run
        │
        ├── Backend chạy mãi...
        │
        └── Terminal bị chiếm

Vì backend không bao giờ kết thúc (nó là server), nên dòng:

npm run dev

sẽ không bao giờ được thực hiện.
```
**Có &**
```bash
mvn spring-boot:run &
npm run dev

mvn spring-boot:run &
        │
        ├── Chạy nền
        └── Terminal tiếp tục

↓

npm run dev

Backend vẫn chạy, nhưng shell tiếp tục chạy lệnh kế tiếp.
```
# wait (Đợi tất cả các tiến trình chạy nền kết thúc rồi mới kết thúc script)
```bash
Nếu không có wait, script sẽ chạy hết các dòng rồi thoát ngay. Trong nhiều trường hợp các tiến trình nền vẫn tiếp tục chạy, nhưng với một số môi trường hoặc khi bạn muốn quản lý chúng tốt hơn, wait giúp script giữ trạng thái và đợi các tiến trình con hoàn thành.

Tóm tắt
command → chạy ở foreground, terminal phải chờ.
command & → chạy ở background, terminal chạy tiếp lệnh khác.
wait → đợi các lệnh chạy nền kết thúc.

Chính vì vậy, trong các script khởi động nhiều service (FastAPI, React, Redis, Spring Boot...), bạn sẽ thấy rất nhiều dấu & để các service được khởi động song song.
```