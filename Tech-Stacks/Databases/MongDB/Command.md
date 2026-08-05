- [Installation](#installation)
---
# Installation
```bash
1. Cài tool cần thiết
    + sudo apt update
    + sudo apt install -y curl gnupg
2. Import key MongoDB
    + curl -fsSL https://pgp.mongodb.com/server-7.0.asc | \ sudo gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor
3. Thêm repo MongoDB
    + echo "deb [ signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] \
https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | \
sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
4. Cài MongoDB
    + sudo apt update
    + sudo apt install -y mongodb-org
5. Khởi động & enable
    + sudo systemctl start mongod
    + sudo systemctl enable mongod
6. Kiểm tra
    + mongosh
```