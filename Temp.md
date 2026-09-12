- [cbow temp](#cbow-temp)
---
1. PySpark là gì?

PySpark là Python API của Spark.

Spark ban đầu được xây dựng chủ yếu bằng Scala/Java.

PySpark cho phép bạn dùng Python để điều khiển Spark.

Ví dụ:

from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("MyPipeline") \
    .getOrCreate()

df = spark.read.json("data.json")

df.filter(df.age > 18).show()

Nếu dùng Pandas:

import pandas as pd

df = pd.read_json("data.json")

df = df[df["age"] > 18]

Ý tưởng khá giống nhau.

Nhưng Spark có khả năng phân tán dữ liệu trên cluster.

# cbow temp
Nếu bạn muốn tự test CBOW/Word2Vec bằng Python, có vài lựa chọn. Với mục tiêu hiểu cơ chế, mình khuyên không nên dùng thư viện ngay từ đầu.

1. Muốn test nhanh → gensim

Thư viện phổ biến nhất cho Word2Vec là Gensim.

pip install gensim

Ví dụ:

from gensim.models import Word2Vec

sentences = [
    ["i", "love", "machine", "learning"],
    ["i", "love", "deep", "learning"],
    ["machine", "learning", "is", "interesting"],
    ["deep", "learning", "is", "powerful"],
]

model = Word2Vec(
    sentences,
    vector_size=100,
    window=2,
    min_count=1,
    sg=0,       # 0 = CBOW
    epochs=100
)

vector = model.wv["learning"]

print(vector)
print(model.wv.most_similar("learning"))

Điểm cần nhớ:

sg=0  # CBOW
sg=1  # Skip-gram
2. Nhưng nếu mục tiêu của bạn là hiểu CBOW

Mình khuyên bạn tự implement bằng PyTorch.

Ví dụ kiến trúc:

Context words
     ↓
Embedding
     ↓
Average
     ↓
Linear
     ↓
Softmax
     ↓
Target

Dùng:

pip install torch

Bạn sẽ tự thấy được:

embedding = nn.Embedding(vocab_size, embedding_dim)

và:

context_vector = embedding(context_words).mean(dim=0)

sau đó:

output = linear(context_vector)

rồi:

loss = CrossEntropyLoss()(output, target)

Train:

loss.backward()
optimizer.step()

Sau khi train:

embedding.weight

chính là nơi bạn có thể nhìn trực tiếp các vector mà model đã học.

3. Nếu học theo hướng của bạn, mình sẽ làm theo thứ tự
                CBOW
                  │
        ┌─────────┴─────────┐
        ↓                   ↓
   Hiểu objective       Hiểu embedding
        │                   │
 Context → Target      Word → Vector
        │                   │
        └─────────┬─────────┘
                  ↓
            Tự code PyTorch
                  ↓
             Gensim test
                  ↓
             Skip-gram
                  ↓
              Word2Vec

Đừng bắt đầu bằng Gensim nếu mục tiêu là hiểu sâu. Gensim sẽ cho bạn kết quả rất nhanh nhưng bạn dễ chỉ biết sg=0 là CBOW mà chưa hiểu bên trong nó chạy thế nào.

Nếu muốn, mình có thể 
viết cho bạn một CBOW cực nhỏ bằng PyTorch, khoảng 30–40 dòng, rồi giải thích từng dòng từ input → embedding → average → predict target → backprop, khá hợp với hướng bạn đang học RNN/Seq2Seq.

# https://blog.bytebytego.com/p/free-system-design-pdf-158-pages

GoF Patterns là viết tắt của Gang of Four Design Patterns — một bộ 23 Design Pattern kinh điển được giới thiệu trong cuốn Design Patterns: Elements of Reusable Object-Oriented Software.

Nếu bạn đang học Java/Spring Boot, đây là một nhóm kiến thức khá quan trọng.

1. Design Pattern là gì?

Hiểu đơn giản:

Design Pattern = một cách thiết kế thường dùng để giải quyết một loại vấn đề lặp đi lặp lại trong code.

Nó không phải thư viện, cũng không phải code copy-paste.

Ví dụ bạn có:

if (type.equals("email")) {
    // gửi email
} else if (type.equals("sms")) {
    // gửi SMS
} else if (type.equals("push")) {
    // gửi notification
}

Ban đầu rất bình thường.

Nhưng nếu hệ thống ngày càng lớn:

email
sms
push
telegram
slack
...

thì if/else sẽ phình to.

Bạn có thể dùng Strategy Pattern để tách từng cách xử lý.

2. GoF có 23 pattern

Chia thành 3 nhóm:

GoF Design Patterns
│
├── Creational
│     ├── Factory
│     ├── Abstract Factory
│     ├── Builder
│     ├── Prototype
│     └── Singleton
│
├── Structural
│     ├── Adapter
│     ├── Bridge
│     ├── Composite
│     ├── Decorator
│     ├── Facade
│     ├── Flyweight
│     └── Proxy
│
└── Behavioral
      ├── Observer
      ├── Strategy
      ├── Command
      ├── State
      ├── Template Method
      ├── Iterator
      ├── Mediator
      ├── Memento
      ├── Chain of Responsibility
      ├── Visitor
      └── Interpreter

Bạn không cần học thuộc 23 cái ngay.

Trong thực tế, Factory, Strategy, Adapter, Observer, Builder, Singleton, Decorator, Facade là những cái rất đáng hiểu trước.

3. Factory Pattern
Vấn đề

Bạn cần tạo object tùy theo loại.

Ví dụ:

Payment payment;

if (type.equals("paypal")) {
    payment = new PaypalPayment();
} else if (type.equals("stripe")) {
    payment = new StripePayment();
} else if (type.equals("momo")) {
    payment = new MomoPayment();
}

Logic tạo object nằm đầy trong business code.

Factory tách việc đó ra:

Payment payment = PaymentFactory.create(type);

Factory:

class PaymentFactory {

    static Payment create(String type) {
        return switch (type) {
            case "paypal" -> new PaypalPayment();
            case "stripe" -> new StripePayment();
            case "momo" -> new MomoPayment();
            default -> throw new IllegalArgumentException();
        };
    }
}

Mental model:

Business Code
     │
     │ create("stripe")
     ▼
 PaymentFactory
     │
     ▼
StripePayment

Factory = giao việc tạo object cho một nơi chuyên trách.

4. Singleton Pattern

Singleton đảm bảo một class chỉ có một instance trong phạm vi thiết kế của nó.

Ví dụ:

class Config {

    private static Config instance;

    private Config() {}

    public static Config getInstance() {
        if (instance == null) {
            instance = new Config();
        }

        return instance;
    }
}

Sử dụng:

Config config = Config.getInstance();

Lần sau:

Config config2 = Config.getInstance();

thì:

config == config2
      ↓
     true
Nhưng có một điểm quan trọng với Spring

Trong Spring Boot, bạn thường không tự viết Singleton như trên.

Spring mặc định quản lý bean theo singleton scope:

@Service
public class UserService {
}

Spring container quản lý instance của UserService.

Vì vậy khi làm Spring Boot, hiểu Singleton Pattern là tốt, nhưng đừng thấy Singleton rồi tự code Singleton bằng tay nếu Spring đã quản lý object đó.

5. Strategy Pattern

Đây là pattern cực kỳ đáng học.

Giả sử hệ thống có nhiều cách thanh toán:

Payment
├── CreditCard
├── Paypal
├── Momo
└── BankTransfer

Tạo interface:

interface PaymentStrategy {
    void pay(double amount);
}

Các implementation:

class CreditCardPayment implements PaymentStrategy {
    public void pay(double amount) {
        System.out.println("Pay by credit card");
    }
}
class PaypalPayment implements PaymentStrategy {
    public void pay(double amount) {
        System.out.println("Pay by Paypal");
    }
}

Service:

class PaymentService {

    private PaymentStrategy strategy;

    PaymentService(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    void pay(double amount) {
        strategy.pay(amount);
    }
}

Sử dụng:

PaymentService service =
    new PaymentService(new PaypalPayment());

service.pay(100);

Muốn đổi sang Credit Card:

PaymentService service =
    new PaymentService(new CreditCardPayment());

Không cần sửa PaymentService.

Mental model

Strategy = cùng một nhiệm vụ nhưng có nhiều cách thực hiện, và ta có thể thay đổi cách thực hiện.

Ví dụ:

PaymentService
      │
      ├── CreditCardStrategy
      ├── PaypalStrategy
      ├── MomoStrategy
      └── BankStrategy
6. Observer Pattern

Observer dùng khi:

Một object thay đổi → nhiều object khác cần được thông báo.

Ví dụ:

Order
  │
  ├── Email Service
  ├── Notification Service
  ├── Analytics Service
  └── Inventory Service

Khi:

Order = PAID

thì nhiều thành phần cần biết.

Observer:

         Order
           │
      notify observers
           │
     ┌─────┼─────┐
     ↓     ↓     ↓
   Email  SMS  Analytics

Ví dụ conceptual:

interface Observer {
    void update(Order order);
}

Các observer:

class EmailObserver implements Observer {
    public void update(Order order) {
        // send email
    }
}
class AnalyticsObserver implements Observer {
    public void update(Order order) {
        // tracking
    }
}

Khi Order thay đổi:

order.notifyObservers();
Trong backend hiện đại

Ý tưởng Observer xuất hiện rất nhiều dưới dạng:

Event Listener
Application Events
Message Queue
Kafka consumers
Pub/Sub

Ví dụ:

Order Service
     │
     │ OrderPaidEvent
     ▼
   Kafka
     │
     ├── Email Service
     ├── Inventory Service
     └── Analytics Service

Đây là tư duy rất gần Observer, dù implementation thực tế có thể không còn là GoF Observer nguyên bản.

7. Adapter Pattern

Adapter giải quyết vấn đề:

Hai interface không tương thích nhưng bạn muốn chúng làm việc với nhau.

Ví dụ hệ thống của bạn cần:

interface PaymentService {
    void pay(double amount);
}

Nhưng thư viện bên ngoài có:

class StripeSDK {
    void makePayment(double money) {
        // ...
    }
}

Bạn không muốn sửa StripeSDK.

Tạo adapter:

class StripeAdapter implements PaymentService {

    private StripeSDK stripe;

    StripeAdapter(StripeSDK stripe) {
        this.stripe = stripe;
    }

    public void pay(double amount) {
        stripe.makePayment(amount);
    }
}

Bây giờ:

Your Application
      │
      │ PaymentService
      ▼
StripeAdapter
      │
      │ makePayment()
      ▼
StripeSDK

Adapter = bộ chuyển đổi interface.

Giống như:

Ổ điện Việt Nam
       ↓
   Adapter
       ↓
Ổ điện chuẩn khác
8. Builder Pattern

Builder rất hay gặp trong Java.

Thay vì:

User user = new User(
    "Thang",
    22,
    "Hanoi",
    "thang@gmail.com",
    true,
    ...
);

rất khó đọc.

Builder:

User user = User.builder()
    .name("Thang")
    .age(22)
    .email("thang@gmail.com")
    .active(true)
    .build();

Mental model:

Builder = xây object phức tạp từng bước.

Trong Java/Spring, Lombok thường hỗ trợ:

@Builder
public class User {
    private String name;
    private int age;
    private String email;
}
9. Decorator Pattern

Decorator cho phép thêm behavior cho object mà không sửa class gốc.

Ví dụ:

Coffee

Bạn muốn:

Coffee
 + Milk
 + Sugar
 + Whipped Cream

Có thể tạo:

Coffee
  ↓
MilkDecorator
  ↓
SugarDecorator
  ↓
CreamDecorator

Trong backend, tư tưởng Decorator xuất hiện trong:

Request
  ↓
Logging
  ↓
Authentication
  ↓
Authorization
  ↓
Business Logic

Middleware/filter/interceptor thường có tư tưởng tương tự, dù không phải mọi middleware đều là GoF Decorator.

10. Facade Pattern

Facade = tạo một interface đơn giản phía trước một hệ thống phức tạp.

Ví dụ bên dưới có rất nhiều service:

PaymentService
InventoryService
ShippingService
NotificationService

Nếu Controller phải gọi tất cả:

payment.pay();
inventory.update();
shipping.create();
notification.send();

thì Controller rất phức tạp.

Facade:

orderFacade.createOrder(order);

Bên trong:

OrderFacade
   │
   ├── PaymentService
   ├── InventoryService
   ├── ShippingService
   └── NotificationService

Facade = che sự phức tạp phía sau một interface đơn giản.

11. Liên hệ với Spring Boot

Điều thú vị là khi bạn làm Spring Boot, bạn đã gặp rất nhiều tư tưởng Design Pattern mà có thể không nhận ra.

Ví dụ:

Spring Boot
│
├── Dependency Injection
│
├── Singleton Bean
│
├── Factory
│
├── Proxy
│
├── Template Method
│
├── Strategy
│
└── Observer / Event

Ví dụ:

@Service
public class UserService {
}

Spring container chịu trách nhiệm tạo và quản lý object.

Bạn không cần:

UserService service = new UserService();

mà Spring inject:

@Autowired
private UserService userService;

Đó là lý do khi học Design Pattern, đừng chỉ học thuộc code của pattern.

Hãy hiểu:

Pattern giải quyết vấn đề thiết kế nào?

12. Cách học GoF hiệu quả

Mình khuyên không học:

Factory là gì?
Singleton là gì?
Observer là gì?
...

theo kiểu học thuộc định nghĩa.

Hãy học theo problem → solution:

Problem
   ↓
Code bắt đầu có vấn đề gì?
   ↓
Pattern giải quyết thế nào?
   ↓
Trade-off là gì?
   ↓
Khi nào KHÔNG nên dùng?

Ví dụ Strategy:

Có rất nhiều if/else
        ↓
Mỗi branch là một algorithm
        ↓
Tách thành các Strategy
        ↓
Service sử dụng interface
        ↓
Dễ thêm algorithm mới

Đó mới là hiểu Pattern.

Nếu bạn đang học Backend/Spring Boot

Mình sẽ ưu tiên thứ tự:

1. Strategy
      ↓
2. Factory
      ↓
3. Adapter
      ↓
4. Builder
      ↓
5. Observer
      ↓
6. Decorator
      ↓
7. Facade
      ↓
8. Proxy
      ↓
9. Singleton

Đặc biệt Strategy + Factory + Adapter + Builder rất đáng nắm chắc trước, vì chúng xuất hiện thường xuyên trong code backend thực tế.

Và một nguyên tắc cực quan trọng:

Design Pattern không phải thứ để nhét vào code cho "có pattern".
Nếu code đơn giản mà bạn cố dùng 5 pattern, code có thể phức tạp hơn chứ không tốt hơn.

. Trước tiên: hiểu toàn bộ roadmap

Có thể nhìn như sau:

Junior
│
├── Viết API đúng
├── Test
├── Git
├── Design Pattern
└── Database cơ bản
        │
        ▼
Junior → Mid
│
├── API Security
├── RAG tốt hơn
├── System Design
├── Cache
├── Queue
├── Database nâng cao
├── Docker / CI/CD / Cloud
└── AI System Scaling
        │
        ▼
Mid → Senior
│
├── Distributed Systems
├── Event-Driven
├── DDD
├── High Availability
├── Performance
├── Observability
└── Security
        │
        ▼
Senior → Lead
│
├── Architecture decisions
├── Technical Leadership
├── Project / Risk management
├── Mentoring
└── Business / Cost

Điểm quan trọng:

Level cao hơn không đơn giản là biết nhiều framework hơn.

Junior thường hỏi:

"Code cái này như thế nào?"

Mid hỏi:

"Thiết kế thế nào để hệ thống chịu được 100.000 request?"

Senior hỏi:

"Tại sao chọn kiến trúc này? Trade-off là gì? Nếu traffic tăng 100 lần thì sao? Chi phí bao nhiêu? Failure mode là gì?"

Lead hỏi thêm:

"Giải pháp này có phù hợp với mục tiêu kinh doanh và khả năng của team không?"

1. API Security & Design

Phần này gồm hai chuyện:

API Design
     +
API Security
1.1 RESTful API là gì?

REST là một phong cách thiết kế API.

Ví dụ hệ thống User.

Không nên thiết kế kiểu:

POST /getUser
POST /createUser
POST /deleteUser

RESTful hơn:

GET    /users
GET    /users/123
POST   /users
PUT    /users/123
PATCH  /users/123
DELETE /users/123

Tư duy:

/users
    │
    ├── GET     → lấy danh sách
    ├── POST    → tạo
    │
/users/123
    │
    ├── GET     → lấy user
    ├── PUT     → thay toàn bộ
    ├── PATCH   → sửa một phần
    └── DELETE  → xóa
HTTP methods
Method	Ý nghĩa
GET	đọc
POST	tạo/thực hiện action
PUT	thay thế resource
PATCH	cập nhật một phần
DELETE	xóa
1.2 RESTful mature model là gì?

Cái này có thể hiểu theo hướng REST trưởng thành hơn, đặc biệt là Richardson Maturity Model.

Có 4 level:

Level 0
↓
HTTP như một tunnel

Level 1
↓
Resources

Level 2
↓
HTTP verbs + status codes

Level 3
↓
Hypermedia / HATEOAS

Trong thực tế backend hiện đại, đa số API doanh nghiệp chủ yếu ở Level 2.

Ví dụ:

GET /users/123

Response:

200 OK

Không tìm thấy:

404 Not Found

Không được phép:

403 Forbidden

Chưa đăng nhập:

401 Unauthorized

Request sai:

400 Bad Request

Server lỗi:

500 Internal Server Error

Đây là thứ bạn nên cực kỳ chắc.

1.3 Authentication vs Authorization

Hai từ này người mới rất dễ nhầm.

Authentication

Bạn là ai?

Ví dụ:

username/password
      ↓
Login
      ↓
Authentication
      ↓
"Đây là user 123"
Authorization

Bạn được phép làm gì?

Ví dụ:

User 123
role = USER

GET /profile       ✅
DELETE /users/999  ❌

Admin:

User 456
role = ADMIN

GET /profile       ✅
DELETE /users/999  ✅

Mental model:

Authentication
      ↓
Who are you?
      ↓
Authorization
      ↓
What can you do?
1.4 JWT

JWT = JSON Web Token.

Ví dụ:

eyJhbGciOiJIUzI1Ni...

Client login:

POST /login
       ↓
username/password
       ↓
Server
       ↓
JWT

Sau đó request:

GET /users/123
Authorization: Bearer <JWT>

Server verify JWT:

JWT
 ↓
verify signature
 ↓
decode claims
 ↓
user_id = 123
role = USER
 ↓
check authorization

JWT thường có:

HEADER.PAYLOAD.SIGNATURE

Ví dụ payload:

{
  "sub": "123",
  "role": "USER",
  "exp": 1780000000
}

Quan trọng: payload JWT thường không được mã hóa để giữ bí mật. Nó chủ yếu được ký để phát hiện sửa đổi.

1.5 OAuth2

OAuth2 giải quyết vấn đề:

Một application muốn được phép truy cập tài nguyên thay mặt user mà không cần biết password của user.

Ví dụ:

Your App
   │
   │ "Tôi muốn truy cập Google Calendar"
   ▼
Google Authorization Server
   │
   │ User login + consent
   ▼
Access Token
   │
   ▼
Your App
   │
   ▼
Google Calendar API

OAuth2 rất phổ biến khi:

Login with Google
Login with GitHub
Login with Microsoft

Nhưng cần phân biệt:

OAuth2 là authorization framework. JWT là token format.

Chúng không phải cùng một thứ.

1.6 RBAC

RBAC = Role-Based Access Control.

Ví dụ:

ADMIN
 ├── create user
 ├── delete user
 ├── view user

MANAGER
 ├── view user
 └── update user

USER
 └── view own profile

Trong API:

DELETE /users/123

Backend kiểm tra:

Authentication
      ↓
user = 456
      ↓
role = USER
      ↓
Authorization
      ↓
DELETE users?
      ↓
❌ 403
2. AI Application — RAG

Đây là phần đặc biệt quan trọng nếu bạn đi theo AI Backend.

RAG:

Retrieval-Augmented Generation

Thay vì:

Question
   ↓
LLM
   ↓
Answer

ta làm:

Question
   ↓
Retrieve relevant documents
   ↓
Context
   ↓
LLM
   ↓
Answer
2.1 Chunking

Một document dài:

100 pages

không nên nhét nguyên vào retrieval.

Ta chia:

Document
│
├── Chunk 1
├── Chunk 2
├── Chunk 3
├── ...
└── Chunk N

Ví dụ:

chunk_size = 500 tokens
overlap = 50 tokens

Chunk 2 sẽ có một phần overlap với Chunk 1.

2.2 Chunking strategies

Không phải lúc nào:

mỗi 500 tokens

cũng tốt.

Có thể chunk theo:

Fixed-size
500 tokens
500 tokens
500 tokens

Đơn giản.

Recursive

Ưu tiên:

document
 ↓
paragraph
 ↓
sentence
 ↓
word

Cố gắng giữ semantic boundary.

Semantic chunking

Dựa vào ý nghĩa:

Topic A
   ↓
Chunk

Topic B
   ↓
Chunk

Không đơn giản chỉ dựa vào số token.

Structure-aware

Ví dụ tài liệu:

Chapter
 ├── Section
 │    ├── Paragraph
 │    └── Table

Ta chunk theo cấu trúc tài liệu.

2.3 Vector Search

Document:

"Python là một ngôn ngữ lập trình..."

Embedding:

[0.12, -0.43, 0.81, ...]

Question:

"Python dùng để làm gì?"

Embedding question:

[0.10, -0.40, 0.79, ...]

Tính similarity.

Question
   ↓
Embedding
   ↓
Vector DB
   ↓
Top K chunks
2.4 BM25

Vector search hiểu semantic meaning.

BM25 thiên về keyword matching.

Ví dụ query:

"Redis connection timeout 500ms"

BM25 rất tốt nếu document chứa chính xác:

Redis
connection
timeout
500ms
2.5 Hybrid Search

Kết hợp:

                Query
                  │
          ┌───────┴────────┐
          ↓                ↓
       BM25             Vector
          ↓                ↓
     keyword          semantic
          │                │
          └───────┬────────┘
                  ↓
             merge/rank
                  ↓
             Top K docs

Đây là một cải tiến rất phổ biến của RAG.

2.6 AI latency optimization

Ví dụ request AI hiện tại:

Request
 ↓
Embedding 300ms
 ↓
Vector Search 100ms
 ↓
Reranker 500ms
 ↓
LLM 3s
 ↓
Response

Total ≈ 3.9s

Bạn cần tìm bottleneck.

Có thể tối ưu:

Embedding cache
Vector DB indexing
Parallel retrieval
Reduce top-K
Streaming LLM response
Smaller model
Batching
Connection pooling

Mục tiêu không chỉ:

"Model trả lời đúng."

mà còn:

"Model trả lời đúng trong thời gian và chi phí chấp nhận được."

3. Junior → Mid: System Design

Đây là bước nhảy rất lớn.

Junior thường xây:

Client
  ↓
Backend
  ↓
Database

Mid bắt đầu suy nghĩ:

Traffic tăng thì sao?
Database chịu nổi không?
Backend chết thì sao?
Cache ở đâu?
Request quá nhiều thì sao?
Service giao tiếp thế nào?
3.1 Caching

Cache = lưu dữ liệu thường dùng ở nơi nhanh hơn.

Không cache:

API
 ↓
PostgreSQL
 ↓
Response

Có cache:

API
 ↓
Redis
 ↓ hit
Response

Nếu cache miss:

API
 ↓
Redis ❌
 ↓
PostgreSQL
 ↓
Redis ← save
 ↓
Response
3.2 Redis vs Memcached

Cả hai đều có thể dùng làm cache.

Redis có nhiều tính năng hơn:

Redis
├── String
├── Hash
├── List
├── Set
├── Sorted Set
├── TTL
├── Pub/Sub
├── Streams
└── ...

Memcached đơn giản hơn, chủ yếu là distributed cache dạng key-value.

Trong backend hiện đại, Redis thường gặp nhiều hơn.

3.3 Load Balancing

Một server:

100,000 users
       ↓
    Server

Không muốn tất cả traffic vào một máy.

Ta có:

                Load Balancer
               /      |      \
              ↓       ↓       ↓
           Server1 Server2 Server3

Load balancer phân phối request.

Nếu:

Server2 ❌

có thể ngừng gửi request tới Server2.

3.4 Message Queue

Có những việc không cần làm ngay.

Ví dụ:

User đăng ký
    ↓
Create account
    ↓
Response ngay

Nhưng gửi email có thể làm sau:

User đăng ký
    ↓
Create account
    ↓
Queue
    ↓
Response

Worker:

Queue
 ↓
Email Worker
 ↓
Send email

Công nghệ:

RabbitMQ
Kafka
SQS
3.5 Kafka vs RabbitMQ

Đừng nghĩ:

Kafka = RabbitMQ nhưng nhanh hơn.

Chúng có tư duy khác nhau.

RabbitMQ

Thường phù hợp:

Producer
   ↓
Queue
   ↓
Consumer

Task/job/message processing.

Kafka

Thiên về:

Event Stream

Ví dụ:

Order Service
      ↓
OrderCreated
      ↓
Kafka
 ┌────┼────┐
 ↓    ↓    ↓
Email Analytics Inventory

Nhiều consumer có thể independently đọc event.

3.6 Monolith

Một application:

Backend
├── User
├── Order
├── Payment
├── Notification
└── AI

Tất cả deploy cùng nhau.

Đây là Monolith.

3.7 Modular Monolith

Vẫn một application:

Application
│
├── User Module
├── Order Module
├── Payment Module
└── AI Module

nhưng code được phân module rõ ràng.

Đây thường là bước trung gian rất tốt.

3.8 Microservices

Tách thành nhiều service:

User Service
Order Service
Payment Service
Notification Service
AI Service

Mỗi service có thể deploy độc lập.

Nhưng complexity tăng rất mạnh:

Network
Failure
Distributed transaction
Monitoring
Deployment
Service discovery
Authentication
Message queue

Cho nên:

Không phải cứ Microservices là tốt hơn Monolith.

4. Database Advanced
4.1 Replication

Có database:

Primary
   │
   ├── Replica 1
   └── Replica 2

Primary xử lý write:

INSERT
UPDATE
DELETE

Replica xử lý read:

SELECT

Mục tiêu:

High Availability
+
Read Scaling
4.2 Sharding

Replication:

Database
 ├── Primary
 ├── Replica
 └── Replica

Sharding thì chia dữ liệu:

Shard 1 → users 1 - 1M
Shard 2 → users 1M - 2M
Shard 3 → users 2M - 3M

Hoặc hash:

hash(user_id) % 3

→ xác định user nằm ở shard nào.

Sharding rất mạnh nhưng rất phức tạp.

4.3 ACID

Database transaction có 4 tính chất:

A = Atomicity
C = Consistency
I = Isolation
D = Durability

Ví dụ chuyển tiền:

A có 100$
B có 0$

Transfer 50$

A -= 50
B += 50

Không được xảy ra:

A -= 50
B += 50 ❌

Nếu B update fail thì transaction cần rollback.

4.4 Saga Pattern

Khi có microservices:

Order Service
Payment Service
Inventory Service
Shipping Service

không dễ dùng một database transaction duy nhất.

Saga chia transaction thành các bước:

Create Order
   ↓
Payment
   ↓
Reserve Inventory
   ↓
Create Shipment

Nếu:

Inventory ❌

thì cần compensation:

Cancel Payment
Cancel Order

Đây gọi là Saga / compensating transaction.

4.5 SQL vs NoSQL

SQL:

PostgreSQL
MySQL

thường mạnh ở:

relationships
transactions
structured data
complex queries

NoSQL:

MongoDB
DynamoDB
Cassandra

có thể phù hợp khi:

scale lớn
schema linh hoạt
access pattern đặc biệt
high throughput

Không có câu:

"NoSQL tốt hơn SQL."

Mà phải hỏi:

"Bài toán này cần đặc tính nào?"

5. DevOps & Cloud
5.1 CI/CD

CI:

Code thay đổi → tự động build/test.

CD:

Code pass → tự động đưa qua các môi trường/deploy.

Ví dụ:

git push
   ↓
GitHub Actions
   ↓
Run tests
   ↓
Build Docker
   ↓
Security scan
   ↓
Push image
   ↓
Deploy

Công cụ:

GitHub Actions
GitLab CI
Jenkins
5.2 AWS VPC

VPC = Virtual Private Cloud.

Bạn có thể hình dung:

AWS
│
└── VPC
    │
    ├── Public Subnet
    │
    └── Private Subnet

Ví dụ:

Internet
   ↓
Load Balancer
   ↓
Public subnet
   ↓
Backend
   ↓
Private subnet
   ↓
Database

Database không cần expose trực tiếp ra Internet.

5.3 ECS / EKS
ECS

AWS quản lý container orchestration.

EKS

AWS managed Kubernetes.

Nếu bạn học Kubernetes thì:

Kubernetes
      ↓
EKS

là một hướng rất tự nhiên.

5.4 Serverless

Không cần tự quản lý server theo kiểu truyền thống.

Ví dụ:

API Gateway
      ↓
Lambda
      ↓
Database

Bạn trả tiền chủ yếu theo usage thay vì duy trì server luôn chạy.

6. AI System Scaling
6.1 Vector Database Indexing

Khi vector database có:

1,000 vectors

brute-force search có thể ổn.

Nhưng:

100 million vectors

thì cần indexing.

6.2 HNSW

HNSW = Hierarchical Navigable Small World.

Ý tưởng:

Vector space

      A------B
     /        \
    C----D-----E

Thay vì so sánh query với mọi vector, index giúp tìm các vector gần nhau hiệu quả hơn.

Trade-off:

speed
   ↕
recall
   ↕
memory
6.3 IVF

IVF = Inverted File Index.

Ý tưởng:

100 million vectors

        ↓ clustering

Cluster 1
Cluster 2
Cluster 3
...
Cluster N

Query:

query
 ↓
tìm cluster gần nhất
 ↓
search trong cluster đó

Không cần search toàn bộ dataset.

6.4 Model Monitoring

Deploy model xong chưa phải kết thúc.

Cần biết:

Latency
Error rate
Token usage
Cost
Quality
Drift
Throughput

Ví dụ:

LLM latency
P50 = 1.2s
P95 = 3.5s
P99 = 8.1s

Nếu P99 tăng lên:

15s

→ cần điều tra.

6.5 MLOps

MLOps = các practices để quản lý vòng đời model/data.

Ví dụ:

Data
 ↓
Training
 ↓
Experiment
 ↓
Model
 ↓
Evaluation
 ↓
Deployment
 ↓
Monitoring

DVC:

version control cho dataset/model artifacts.

MLflow:

tracking experiments, metrics, models, model registry...

7. Mid → Senior: High-Level Architecture

Đây là bước bắt đầu chuyển từ:

"Tôi biết code"

sang:

"Tôi hiểu hệ thống phân tán."

7.1 Event-Driven Architecture

Thay vì service gọi trực tiếp:

Order
 ↓
Payment
 ↓
Inventory
 ↓
Email

có thể:

Order
 ↓
OrderCreated Event
 ↓
Kafka
 ├── Payment
 ├── Inventory
 └── Email

Các service giảm coupling.

7.2 DDD

DDD = Domain-Driven Design.

Tập trung thiết kế software dựa trên business domain.

Ví dụ e-commerce:

Order
Payment
Inventory
Shipping
Customer

DDD giúp trả lời:

"Business thực sự được chia thành những domain nào?"

Một khái niệm quan trọng:

Bounded Context

E-commerce
│
├── Order Context
├── Payment Context
├── Inventory Context
└── Shipping Context

Đây là tư duy rất hữu ích khi thiết kế microservices.

7.3 Distributed Systems Consensus

Khi có nhiều server:

Node A
Node B
Node C

làm sao chúng đồng ý:

"Ai là leader?"

hoặc:

"Giá trị nào là đúng?"

Đây là bài toán consensus.

Các thuật toán nổi tiếng:

Raft
Paxos

Bạn chưa cần tự implement ngay.

Quan trọng là hiểu:

Network can fail
Node can fail
Messages can delay
Nodes can disagree

và hệ thống phải xử lý thế nào.

8. Performance Tuning

Đây là một bước rất khác.

Junior:

"API này chạy được."

Mid:

"API này chạy 200ms."

Senior:

"Tại sao nó mất 200ms? 150ms nằm ở DB hay network hay CPU?"

8.1 Profiling

Ví dụ:

Request = 500ms

Database       50ms
Redis          10ms
Network        40ms
Python CPU    400ms

Bạn không nên tối ưu database.

Bottleneck nằm ở Python.

Profiling giúp tìm:

CPU bottleneck
Memory bottleneck
I/O bottleneck
Lock contention
Network bottleneck
8.2 CPython memory

Python có:

reference counting
garbage collector
object overhead

Ví dụ bạn tạo:

users = [
    {"name": "..."}
    for _ in range(10_000_000)
]

Có thể tiêu tốn memory rất lớn.

Senior Python engineer cần hiểu:

heap
object allocation
GC
reference
memory profiling
8.3 JVM tuning

Với Java/Spring Boot:

JVM
 │
 └── Heap
      ├── Young Generation
      └── Old Generation

Garbage Collector:

G1
ZGC
...

Nếu application:

GC pause
CPU
memory

không ổn, cần profiling/tuning.

9. Observability

Đây là thứ cực kỳ quan trọng khi hệ thống lớn.

Có 3 trụ cột:

Observability
│
├── Logs
├── Metrics
└── Traces
9.1 Logging

Ví dụ:

2026-09-10
ERROR
payment failed
order_id=123

Tool:

ELK
Elasticsearch
Logstash
Kibana
9.2 Metrics

Metrics là số liệu.

Ví dụ:

HTTP requests/sec
CPU usage
Memory
Error rate
Latency

Prometheus thu thập metrics.

Grafana visualize:

Request Rate
████████████████

Error Rate
██

Latency
██████
9.3 Distributed Tracing

Một request:

Frontend
 ↓
API Gateway
 ↓
Order Service
 ↓
Payment Service
 ↓
Database

Nếu request mất 5 giây, làm sao biết 4 giây nằm ở đâu?

Tracing:

Trace ID = abc123

Gateway       20ms
Order        100ms
Payment     3800ms   ← bottleneck
Database      80ms

Jaeger là một tracing system.

10. Security & Compliance
10.1 OWASP Top 10

Đây là nhóm rủi ro bảo mật web phổ biến.

Ví dụ:

Broken Access Control
Injection
Security Misconfiguration
Cryptographic Failures
...

Bạn đã học một số thứ liên quan:

SQL Injection
Authentication
Authorization
JWT
Cookies

nên đây là bước tiếp theo rất hợp lý.

10.2 Encryption in transit

Dữ liệu:

Client
  ↓
HTTPS/TLS
  ↓
Server

Không gửi password plaintext qua HTTP.

10.3 Encryption at rest

Database/disk chứa dữ liệu được mã hóa:

Database
   ↓
Encrypted storage

Nếu attacker lấy được disk/storage thì dữ liệu vẫn khó đọc hơn.

11. Senior → Lead

Ở đây bắt đầu có một thay đổi lớn:

Senior
    ↓
giải quyết vấn đề kỹ thuật khó

Lead
    ↓
giúp cả team giải quyết vấn đề đúng
11.1 Code Review

Không chỉ:

Code chạy không?

mà xem:

Correctness
Security
Performance
Maintainability
Testability
Architecture
11.2 RFC

RFC = Request for Comments.

Ví dụ team muốn chọn:

RabbitMQ vs Kafka

Bạn viết document:

Problem
Requirements
Option A
Option B
Trade-offs
Cost
Recommendation
Migration Plan

Team review trước khi implement.

Đây là cách đưa technical decision ra khỏi "ý kiến cá nhân".

11.3 Technical Debt

Technical debt = những quyết định kỹ thuật nhanh/không tối ưu hôm nay tạo ra chi phí bảo trì ngày mai.

Ví dụ:

Hôm nay:
Hard-code config

→ nhanh.

Sau 1 năm:

50 nơi hard-code
 ↓
khó maintain
 ↓
technical debt

Lead cần quyết định:

Nợ nào phải trả ngay?
Nợ nào có thể chấp nhận?
12. Agile / Scrum

Không chỉ là:

Daily meeting

Mà gồm:

Planning
↓
Development
↓
Review
↓
Retrospective
12.1 Estimation

Ví dụ một feature:

OAuth login

Không chỉ:

"3 ngày."

Mà phân tích:

Backend       1 day
Frontend      1 day
Testing       0.5 day
Integration   0.5 day
Risk          ?

Estimation tốt phải tính:

complexity
dependencies
unknowns
risk
12.2 Risk Management

Ví dụ project AI:

RAG system

Risk:

Vector DB scale?
LLM API outage?
LLM cost?
Latency?
Hallucination?
Data privacy?

Senior/Lead phải nhìn thấy những rủi ro này trước khi production gặp vấn đề.

13. People Management

Đây là phần không còn thuần technical.

Lead phải giúp Junior:

Junior
 ↓
code review
 ↓
feedback
 ↓
mentoring
 ↓
Junior tiến bộ

Ngoài ra:

Recruitment
Conflict resolution
Communication
Delegation
Career development
14. Business Perspective

Đây là khác biệt rất lớn giữa Senior Engineer và người có tư duy Lead.

Giả sử có hai phương án.

Option A
3 tháng
$100k
99.99% availability
Option B
2 tuần
$10k
99.9% availability

Nếu startup chỉ có:

100 users

thì Option A có thể là over-engineering.

Nhưng nếu:

banking/payment
10 million users

thì Option B có thể không đủ.

Cho nên câu hỏi không phải:

"Kiến trúc nào xịn hơn?"

Mà:

"Kiến trúc nào phù hợp với business requirement?"

15. FinOps

FinOps = quản lý chi phí cloud dựa trên usage/business.

Ví dụ AWS:

EC2        $2,000
RDS        $1,000
S3           $100
EKS          $800
LLM API    $5,000
-----------------
Total      $8,900/month

Senior/Lead phải biết hỏi:

Tại sao LLM tốn $5k?
Có cache được không?
Model nhỏ hơn được không?
Batch request được không?
Reserved instance?
Autoscaling?
16. Time-to-market vs Technical Quality

Đây là trade-off cực kỳ thực tế.

Ví dụ:

Feature cần release trong 2 tuần

Bạn có hai lựa chọn:

A: Perfect architecture
   3 tháng

B: Good enough architecture
   2 tuần

Không phải lúc nào A cũng đúng.

Có thể chọn:

B
↓
ship
↓
monitor
↓
learn
↓
refactor khi cần

Nhưng cũng không nên:

ship nhanh
↓
hack
↓
hack
↓
hack
↓
production sập

Đó là lý do cần cân bằng:

Business
   ↕
Time-to-market
   ↕
Technical Quality
   ↕
Cost
   ↕
Risk
17. Nếu gom tất cả lại thành một hệ thống

Bạn có thể hình dung một backend production lớn như sau:

                    Internet
                       │
                       ▼
                Load Balancer
                       │
                       ▼
                 API Gateway
                       │
          ┌────────────┼────────────┐
          ▼            ▼            ▼
      User Service  Order Service  AI Service
          │            │            │
          ▼            ▼            ▼
       Redis        PostgreSQL    Vector DB
          │            │            │
          │            │            ├── BM25
          │            │            ├── Vector Search
          │            │            └── LLM
          │            │
          └────────────┼──────────────┐
                       ▼              │
                    Kafka             │
                       │              │
              ┌────────┼────────┐     │
              ▼        ▼        ▼     │
           Email   Analytics Inventory│
                                      │
                       Observability  │
                    ┌──────┼──────┐   │
                    ▼      ▼      ▼   │
                  Logs Metrics Traces │
                                      │
                       CI/CD          │
                         │            │
                    GitHub Actions    │
                         │            │
                       Docker        │
                         │            │
                       EKS           │
                         │            │
                        AWS           │

Đây chính là nơi tất cả những keyword trong roadmap bắt đầu kết nối với nhau.

18. Nhưng bạn không nên học tất cả cùng lúc

Nếu mục tiêu của bạn hiện tại là Backend + AI Engineer, mình sẽ chia thành các tầng:

Tầng 1 — phải cực chắc
Python / Java
HTTP
REST API
FastAPI / Spring Boot
SQL
Git
Testing
Docker
Authentication
Authorization
Tầng 2 — Junior → Mid
Redis
PostgreSQL advanced
JWT / OAuth2
RBAC
Message Queue
Kafka
System Design
CI/CD
Docker Compose
AWS basics
Tầng 3 — AI Backend
RAG
Chunking
Embedding
Vector Search
BM25
Hybrid Search
Reranking
Vector DB
LLM inference
Caching
Latency optimization
Evaluation
Tầng 4 — Mid → Senior
Microservices
Event-driven architecture
DDD
Distributed systems
Replication
Sharding
Saga
Observability
Performance profiling
High Availability
Security
Tầng 5 — Senior → Lead
Architecture decision
RFC
Technical Debt
Mentoring
Estimation
Risk
FinOps
Business trade-off
Team leadership
Và có một điều mình muốn nhấn mạnh

Với những thứ bạn đang học như REST → JWT/Cookie/PASETO → gRPC → Docker → Kubernetes → LangGraph/RAG → Git → Testing, thực ra bạn đang đi đúng theo chiều ngang của roadmap này.

Bước tiếp theo không phải là học thuộc thêm 50 công nghệ.

Bạn nên bắt đầu ghép chúng thành một project production-like, ví dụ:

                    Frontend
                       │
                       ▼
                FastAPI / Spring
                       │
              ┌────────┴────────┐
              ▼                 ▼
        PostgreSQL            Redis
              │
              ▼
         AI/RAG Service
              │
        ┌─────┴─────┐
        ▼           ▼
    BM25 Search  Vector DB
        │           │
        └─────┬─────┘
              ▼
             LLM
              │
              ▼
           Response

        Kafka / RabbitMQ
              │
       Background Worker

        GitHub Actions
              │
           Docker
              │
        Kubernetes/EKS

     Prometheus + Grafana
     Logs + Distributed Trace

Khi bạn tự thiết kế, code, test, Dockerize, deploy và debug một hệ thống như vậy, các keyword như RESTful, OAuth2, RBAC, Redis, Kafka, RAG, HNSW, CI/CD, Kubernetes, Observability, Saga... sẽ không còn là những thuật ngữ rời rạc nữa. Bạn sẽ hiểu tại sao người ta cần chúng và khi nào nên dùng chúng.