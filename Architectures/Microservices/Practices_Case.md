# Demo Cấu trúc chuẩn microservice với Python + nodeJs
**Flow Chart**
```bash
Browser (HTML + JS)
        |
        | fetch()
        v
NodeJS API Gateway :3000
        |
        | HTTP
        +--> Python User Service  :8001
        |
        +--> Python Order Service :8002
```
**Cây thư mục**
```bash
microservice-demo/
│
├── frontend/
│   └── index.html
│
├── gateway/
│   ├── server.js
│   └── package.json
│
├── user-service/
│   ├── main.py
│   └── requirements.txt
│
├── order-service/
│   ├── main.py
│   └── requirements.txt
```
**user-service/requirements.txt**
```bash
fastapi
uvicorn
```
**user-service/main.py**
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/users/{user_id}")
def get_user(user_id: int):
    return {
        "id": user_id,
        "name": "Thang",
        "email": "thang@example.com"
    }

# cd user-service
# pip install -r requirements.txt
# uvicorn main:app --port 8001
# test nhanh: http://localhost:8001/users/1
```
**order-service/requirements.txt**
```bash
fastapi
uvicorn
```
**order-service/main.py**
```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/orders/{user_id}")
def get_orders(user_id: int):
    return [
        {"id": 1, "item": "Laptop"},      
        {"id": 2, "item": "Mouse"}
    ]

# cd order-service
# pip install -r requirements.txt
# uvicorn main:app --port 8002
# test nhanh: http://localhost:8002/orders/1
```
**gateway/package.json**
```json
{
  "name": "api-gateway",
  "version": "1.0.0",
  "dependencies": {
    "axios": "^1.6.0",
    "express": "^4.18.2",
    "cors": "^2.8.5"
  }
}
```
**gateway/server.js**
```js
const express = require("express");
const axios = require("axios");
const cors = require("cors");

const app = express();
app.use(cors());

app.get("/api/profile/:id", async (req, res) => {
  const userId = req.params.id;

  try {
    const userRes = await axios.get(
      `http://localhost:8001/users/${userId}`
    );

    const orderRes = await axios.get(
      `http://localhost:8002/orders/${userId}`
    );

    res.json({
      user: userRes.data,
      orders: orderRes.data
    });
  } catch (err) {
    res.status(500).json({
      error: "One of services is down",
      detail: err.message
    });
  }
});

app.listen(3000, () => {
  console.log("API Gateway running at http://localhost:3000");
});

// cd gateway
// npm install
// node server.js
// test nhanh: http://localhost:3000/api/profile/1
```
**frontend/index.html**
```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Microservice Demo</title>
</head>
<body>
  <h1>Fake Frontend</h1>

  <button onclick="loadProfile()">Load User Profile</button>

  <pre id="output"></pre>

  <script>
    async function loadProfile() {
      const res = await fetch("http://localhost:3000/api/profile/1");
      const data = await res.json();
      document.getElementById("output").textContent =
        JSON.stringify(data, null, 2);
    }
  </script>
</body>
</html>
```