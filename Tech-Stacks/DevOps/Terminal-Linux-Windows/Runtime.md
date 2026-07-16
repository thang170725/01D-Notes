- [.sh (shell script - một file chứa nhiều lệnh terminal được viết sẵn để chạy tự động)](#sh-shell-script---một-file-chứa-nhiều-lệnh-terminal-được-viết-sẵn-để-chạy-tự-động)
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
giờ tôi mới thấy sh khá mạnh trước tôi chạy web tôi cần phải mở 2 terminal 1 backend, 1 frontend, vậy thì mình có thể cấu hình cả 2 cái này vào sh để chạy 1 lệnh được không nhỉ
Đúng vậy. Đó chính là một trong những lý do .sh được dùng rất nhiều trong thực tế. Bạn hoàn toàn có thể khởi động cả backend và frontend chỉ bằng một lệnh.

Ví dụ cấu trúc dự án:

my-project/
├── backend/
│   └── pom.xml
├── frontend/
│   └── package.json
└── start.sh

start.sh

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

Cấp quyền:

chmod +x start.sh

Chạy:

./start.sh

Script sẽ:

chạy backend ở nền (&)
chạy frontend ở nền (&)
wait để script không kết thúc ngay.
Nếu backend của bạn là FastAPI

Thì chỉ cần đổi lệnh:

cd backend
uvicorn main:app --reload &

Frontend React:

cd frontend
npm run dev &
Thực tế còn làm được nhiều hơn

Ví dụ tự kiểm tra và cài dependency:

#!/bin/bash

echo "Install frontend dependencies..."
cd frontend
npm install

echo "Start frontend..."
npm run dev &

cd ../backend

echo "Install backend dependencies..."
pip install -r requirements.txt

echo "Start backend..."
uvicorn main:app --reload &

Hoặc với Java:

#!/bin/bash

echo "Build backend..."
cd backend
mvn clean package

echo "Run backend..."
java -jar target/app.jar &
Thậm chí có thể dừng cả hai

Ví dụ:

#!/bin/bash

pkill -f "spring-boot:run"
pkill -f "vite"

hoặc lưu PID rồi kill đúng tiến trình.

Nhưng trong các dự án lớn, người ta thường dùng gì?

.sh rất hữu ích, nhưng khi dự án lớn hơn, nhiều nhóm sẽ dùng các công cụ chuyên biệt:

Docker Compose: khởi động backend, frontend, database, Redis... cùng lúc.
Makefile: gom nhiều lệnh thành các mục tiêu như make start, make test, make build.
npm scripts: với dự án JavaScript/TypeScript.
Maven/Gradle: cho các tác vụ liên quan đến Java.

Ví dụ một Makefile:

start:
	cd backend && mvn spring-boot:run &
	cd frontend && npm run dev

Sau đó chỉ cần:

make start

Với dự án AI + FastAPI + React như bạn đang làm, mình thường thấy các nhóm tạo một start.sh hoặc dev.sh để:

Khởi động Redis.
Khởi động backend FastAPI.
Khởi động frontend React/Vite.
In ra địa chỉ truy cập (ví dụ http://localhost:5173 và http://localhost:8000).

Chỉ cần chạy:

./dev.sh

là toàn bộ môi trường phát triển sẵn sàng. Đây là cách làm rất phổ biến trên Linux và macOS.
sao có & ở đằng sau làm gì
Dấu & trong shell có ý nghĩa là:

Chạy lệnh ở background (chạy nền), để terminal không phải chờ lệnh đó kết thúc.

Đây là lý do tại sao bạn có thể chạy nhiều chương trình cùng lúc.

Không có &

Ví dụ:

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

Có &
mvn spring-boot:run &
npm run dev

Lúc này:

mvn spring-boot:run &
        │
        ├── Chạy nền
        └── Terminal tiếp tục

↓

npm run dev

Backend vẫn chạy, nhưng shell tiếp tục chạy lệnh kế tiếp.

Ví dụ đơn giản

Chạy:

sleep 10
echo "Hello"

Bạn sẽ phải đợi 10 giây mới thấy:

Hello

Thêm &:

sleep 10 &
echo "Hello"

Kết quả:

Hello

xuất hiện ngay lập tức, còn sleep vẫn đang chạy nền.

Trong script của bạn
#!/bin/bash

cd backend
mvn spring-boot:run &

cd ../frontend
npm run dev &

Diễn ra như sau:

Backend
    │
    ├── chạy nền
    ▼
Frontend
    │
    ├── chạy nền
    ▼
Script kết thúc (hoặc wait)

Nếu bỏ dấu & ở backend:

mvn spring-boot:run

cd ../frontend
npm run dev

thì shell sẽ kẹt ở backend, không bao giờ chạy đến frontend.

Kiểm tra các tiến trình chạy nền

Gõ:

jobs

Ví dụ:

[1]- Running mvn spring-boot:run &
[2]+ Running npm run dev &

Hoặc xem toàn bộ tiến trình:

ps
wait để làm gì?

Trong ví dụ mình viết:

mvn spring-boot:run &
npm run dev &

wait

wait có nghĩa là:

"Đợi tất cả các tiến trình chạy nền kết thúc rồi mới kết thúc script."

Nếu không có wait, script sẽ chạy hết các dòng rồi thoát ngay. Trong nhiều trường hợp các tiến trình nền vẫn tiếp tục chạy, nhưng với một số môi trường hoặc khi bạn muốn quản lý chúng tốt hơn, wait giúp script giữ trạng thái và đợi các tiến trình con hoàn thành.

Tóm tắt
command → chạy ở foreground, terminal phải chờ.
command & → chạy ở background, terminal chạy tiếp lệnh khác.
wait → đợi các lệnh chạy nền kết thúc.

Chính vì vậy, trong các script khởi động nhiều service (FastAPI, React, Redis, Spring Boot...), bạn sẽ thấy rất nhiều dấu & để các service được khởi động song song.