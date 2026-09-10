Kubernetes (K8s) là một hệ thống dùng để quản lý và vận hành các ứng dụng chạy bằng container trên nhiều máy chủ.

Nói cực đơn giản:

Docker giúp bạn đóng gói và chạy container. Kubernetes giúp bạn quản lý hàng trăm/hàng nghìn container đó.

1. Hãy bắt đầu từ vấn đề thực tế

Giả sử bạn có backend:

FastAPI

Bạn đóng gói nó thành Docker:

┌─────────────────────┐
│ Docker Container    │
│                     │
│ FastAPI             │
│ Python              │
│ Dependencies        │
└─────────────────────┘

Lúc đầu chỉ có 1 container.

Bạn chạy:

docker run my-backend

Không vấn đề gì.

Nhưng khi hệ thống có nhiều người dùng:

100 users
1000 users
10000 users

1 container có thể không đủ.

Bạn có thể chạy:

Container 1
Container 2
Container 3
Container 4

để chia tải.

Nhưng bắt đầu xuất hiện vấn đề:

Container nào chết?
Làm sao tự khởi động lại?
Có 10 container thì request gửi vào container nào?
Làm sao tăng từ 4 → 20 container?
Một server chết thì làm gì?
Deploy version mới như thế nào?
Làm sao update mà người dùng không bị downtime?

Kubernetes sinh ra để giải quyết những vấn đề kiểu này.

2. Kubernetes đứng ở đâu?

Bạn có thể hình dung:

                Kubernetes
                     │
       ┌─────────────┼─────────────┐
       │             │             │
       ▼             ▼             ▼
    Server 1      Server 2      Server 3
       │             │             │
   ┌───┴───┐      ┌───┴───┐      ┌───┴───┐
   │       │      │       │      │       │
 Backend Backend Backend Backend Backend Backend

Kubernetes quản lý các container đang chạy trên những server này.

3. Kubernetes không phải Docker

Đây là chỗ người mới rất dễ nhầm.

Docker

Docker chủ yếu giúp:

Code
 ↓
Docker Image
 ↓
Container
 ↓
Run

Ví dụ:

docker run my-backend
Kubernetes

Kubernetes quản lý:

Container
Container
Container
Container
...

trên nhiều máy.

Ví dụ bạn nói với Kubernetes:

"Tôi muốn backend này luôn có 3 instance đang chạy."

Kubernetes sẽ cố đảm bảo:

Backend #1   ✅
Backend #2   ✅
Backend #3   ✅

Nếu:

Backend #2   💥 chết

Kubernetes phát hiện và tạo lại:

Backend #1   ✅
Backend #2   💥
Backend #3   ✅
Backend #4   🆕

Đây gọi là self-healing.

4. Pod là gì?

Khi học Kubernetes, từ đầu tiên bạn sẽ gặp là:

Pod

Đừng hiểu Pod = Container hoàn toàn.

Đơn giản hóa:

Pod
 └── Container

Thông thường một Pod chứa một container.

Ví dụ:

Pod
└── FastAPI container

Bạn có:

3 Pod

thì có thể là:

Pod 1 → FastAPI
Pod 2 → FastAPI
Pod 3 → FastAPI
5. Deployment là gì?

Bạn không muốn tự tạo từng Pod.

Bạn nói với Kubernetes:

replicas: 3

Nghĩa là:

"Tôi muốn có 3 bản sao ứng dụng."

Kubernetes tạo:

Deployment
    │
    ├── Pod 1
    ├── Pod 2
    └── Pod 3

Nếu Pod chết:

Deployment
    │
    ├── Pod 1 ✅
    ├── Pod 2 💥
    └── Pod 3 ✅

Kubernetes tạo Pod mới:

Deployment
    │
    ├── Pod 1 ✅
    ├── Pod 2 🆕
    └── Pod 3 ✅
6. Service là gì?

Giả sử bạn có:

Pod 1
Pod 2
Pod 3

IP của Pod có thể thay đổi.

Không thể để frontend gọi thẳng:

http://10.2.1.15

vì Pod có thể chết rồi tạo Pod mới với IP khác.

Kubernetes có Service.

              Service
                 │
       ┌─────────┼─────────┐
       ▼         ▼         ▼
     Pod 1     Pod 2     Pod 3

Client chỉ cần gọi:

backend-service

Service sẽ phân phối request tới các Pod.

Đây cũng là một dạng load balancing.

7. Ví dụ với hệ thống của bạn

Giả sử hiện tại bạn có:

Frontend
   │
   ▼
FastAPI
   │
   ├── LangGraph
   ├── Gemini
   ├── MariaDB
   └── Redis

Khi hệ thống lớn hơn, bạn có thể tách:

                    Kubernetes
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
      Frontend       API Service     AI Service
       Pods             Pods            Pods
          │              │              │
          │              │              ▼
          │              │          LangGraph
          │              │
          │              ├──────→ MariaDB
          │              │
          │              └──────→ Redis

Ví dụ:

API Service
replicas = 3

Kubernetes chạy:

API Pod 1
API Pod 2
API Pod 3

Nếu traffic tăng:

3 Pods
   ↓
10 Pods

Nếu traffic giảm:

10 Pods
   ↓
3 Pods

Cơ chế này gọi là scaling.

8. Kubernetes giải quyết những việc gì?

Bạn có thể nhớ 7 nhóm chính:

① Scheduling

Quyết định:

Pod này chạy trên server nào?

Node 1
Node 2
Node 3
② Scaling

Ví dụ:

replicas: 3

→ chạy 3 Pod.

Có thể scale:

3 → 10 → 50
③ Self-healing

Pod chết:

💥

Kubernetes:

🆕

tạo lại.

④ Load balancing

Có:

Pod 1
Pod 2
Pod 3

Request:

Request 1 → Pod 1
Request 2 → Pod 2
Request 3 → Pod 3
⑤ Rolling update

Bạn đang chạy:

Version 1

Deploy:

Version 2

Kubernetes có thể từ từ thay:

V1 V1 V1
 ↓
V2 V1 V1
 ↓
V2 V2 V1
 ↓
V2 V2 V2

thay vì tắt toàn bộ hệ thống cùng lúc.

⑥ Service discovery

Service A muốn gọi Service B:

Order Service
      │
      ▼
User Service

Kubernetes cung cấp cơ chế để các service tìm thấy nhau thông qua Service/DNS.

⑦ Configuration / Secrets

Ví dụ:

DATABASE_URL
GOOGLE_API_KEY
REDIS_URL

Kubernetes có:

ConfigMap
Secret

để quản lý configuration và secret theo cách phù hợp với môi trường container.

9. Kubernetes Cluster là gì?

Một Kubernetes cluster thường gồm:

Kubernetes Cluster
│
├── Control Plane
│
└── Worker Nodes
Control Plane

Có thể coi là bộ não.

Nó quyết định:

Pod nào chạy ở đâu?
Có đủ replicas không?
Pod nào chết?
Deployment hiện tại là version nào?
Worker Node

Là những máy thực sự chạy workload:

Node 1
 ├── Pod
 ├── Pod
 └── Pod

Node 2
 ├── Pod
 ├── Pod
 └── Pod
10. Một ví dụ hoàn chỉnh

Bạn có backend Docker image:

my-backend:v1

Bạn bảo Kubernetes:

replicas: 3
image: my-backend:v1

Kubernetes tạo:

                 Service
                    │
          ┌─────────┼─────────┐
          ▼         ▼         ▼
        Pod 1     Pod 2     Pod 3
          │         │         │
       backend   backend   backend
          │         │         │
          └─────────┼─────────┘
                    │
                 Database

User gửi 1000 request:

                    Internet
                       │
                       ▼
                    Service
                       │
             ┌─────────┼─────────┐
             ▼         ▼         ▼
           Pod 1     Pod 2     Pod 3

Pod 2 chết:

Pod 1 ✅
Pod 2 💥
Pod 3 ✅

Kubernetes tạo:

Pod 1 ✅
Pod 2 🆕
Pod 3 ✅

Traffic tăng:

3 Pods
   ↓
10 Pods

Deploy version mới:

v1 v1 v1
 ↓
v2 v1 v1
 ↓
v2 v2 v1
 ↓
v2 v2 v2

Đó chính là sức mạnh của Kubernetes.

11. Vậy Docker → Kubernetes như thế nào?

Bạn có thể hình dung cả chuỗi:

             Developer
                 │
                 ▼
              Source Code
                 │
                 ▼
              Dockerfile
                 │
                 ▼
             Docker Image
                 │
                 ▼
           Kubernetes
                 │
        ┌────────┼────────┐
        ▼        ▼        ▼
      Pod      Pod      Pod
        │        │        │
        └────────┼────────┘
                 ▼
              Service
                 │
                 ▼
              Users

Docker:

"Đóng gói ứng dụng thành container."

Kubernetes:

"Tôi sẽ quản lý hàng đống container này."

12. Và nó liên quan thế nào tới gRPC?

Cái này nối trực tiếp với câu hỏi trước của bạn.

Giả sử:

Kubernetes Cluster
│
├── API Service
│      ├── Pod 1
│      ├── Pod 2
│      └── Pod 3
│
├── User Service
│      ├── Pod 1
│      └── Pod 2
│
└── AI Service
       ├── Pod 1
       ├── Pod 2
       └── Pod 3

API Service muốn gọi AI Service:

API Service
     │
     │ gRPC
     ▼
AI Service

Kubernetes giúp:

AI Service
     │
     ├── Pod 1
     ├── Pod 2
     └── Pod 3

còn gRPC giúp API Service giao tiếp với AI Service.

Nói cách khác:

Docker
  ↓
đóng gói

Kubernetes
  ↓
quản lý / scale / deploy / network

gRPC
  ↓
giao tiếp giữa các service

Ba thứ này thường xuất hiện cùng nhau trong hệ thống microservices.

13. Nếu bạn đang học Backend thì nên hiểu theo thứ tự này

Mình khuyên học:

1. HTTP
   ↓
2. REST API
   ↓
3. Docker
   ↓
4. Docker Compose
   ↓
5. Microservices
   ↓
6. gRPC + Protobuf
   ↓
7. Kubernetes
   ↓
8. CI/CD
   ↓
9. Cloud (AWS/GCP/Azure)

Đặc biệt Docker Compose → Kubernetes là bước chuyển rất dễ hiểu:

Docker Compose
    ↓
"Chạy vài container trên một máy"

Kubernetes
    ↓
"Quản lý rất nhiều container
trên nhiều máy"

Nếu bạn hiểu được Pod → Deployment → Service → Ingress → Node → Cluster, thì gần như bạn đã có bộ khung tư duy ban đầu để đọc một project Kubernetes rồi.