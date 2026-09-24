+ [<<Back](..)
- [Directory Structure](#directory-structure)
- [Jose Introduction (dùng để làm việc với các chuẩn JOSE đặc biết là JWT)](#jose-introduction-dùng-để-làm-việc-với-các-chuẩn-jose-đặc-biết-là-jwt)
- [Installation](#installation)
---
# Directory Structure
Jose/                      ```mình dùng thư mục này để xem kiến thức cơ bản về Jose```  
└── [Process](Process.md)  ```mình dùng file này để xem cách lệnh trong jose```

# Jose Introduction (dùng để làm việc với các chuẩn JOSE đặc biết là JWT)
```bash
jose không chỉ có JWT. JOSE là một nhóm các chuẩn liên quan đến JSON và cryptography:
    JOSE
    ├── JWS  → JSON Web Signature
    ├── JWE  → JSON Web Encryption
    ├── JWK  → JSON Web Key
    └── JWT  → JSON Web Token
```
# Installation
```bash
1. pip install python-jose | pip install python-jose[cryptography]
```