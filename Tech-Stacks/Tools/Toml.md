+ [<<Back](Base.md)
- [Toml Introduction (thường dùng để cấu hình project)](#toml-introduction-thường-dùng-để-cấu-hình-project)
- [Ask](#ask)
  - [toml không chỉ dành cho Python](#toml-không-chỉ-dành-cho-python)
  - [Tại sao Python hay dùng pyproject.toml?](#tại-sao-python-hay-dùng-pyprojecttoml)
  - [TOML khác JSON/YAML thế nào?](#toml-khác-jsonyaml-thế-nào)
---
# Toml Introduction (thường dùng để cấu hình project)
```bash
Nó giống một file .json, .yaml, .ini nhưng có cú pháp riêng, khá dễ đọc.
```
**Ex**
```bash
Bạn có thể có:
  Bootstrap_project/
  ├── pyproject.toml
  ├── README.md
  ├── .gitignore
  └── src/

Trong đó pyproject.toml có thể chứa:
[project]
name = "bootstrap-project"
version = "0.1.0"
description = "Project bootstrap tool"
requires-python = ">=3.11"

dependencies = [
    "requests",
    "pandas",
]

Nó nói cho Python/tooling biết:
  - Tên project là gì
  - Version bao nhiêu
  - Python tối thiểu là bao nhiêu
  - Project cần những thư viện nào
```
# Ask
## toml không chỉ dành cho Python
```bash
TOML là một định dạng configuration.

Ví dụ:
[database]
host = "localhost"
port = 5432
username = "admin"

[server]
host = "0.0.0.0"
port = 8000
debug = true

Có thể hiểu: TOML -> File cấu hình -> Chương trình đọc cấu hình này
```
## Tại sao Python hay dùng pyproject.toml?
```bash
Ngày trước Python thường có:
  - requirements.txt
  - setup.py
  - setup.cfg

Hiện nay pyproject.toml trở thành một nơi chuẩn để khai báo metadata và cấu hình build/tooling của Python project.

Ví dụ:
[project]
name = "my-project"
version = "0.1.0"
requires-python = ">=3.11"

dependencies = [
    "pandas",
    "numpy",
]

-> Sau đó các tool như package manager/build tool/linter/formatter có thể đọc cấu hình từ đó.
```
## TOML khác JSON/YAML thế nào?
```bash
Ví dụ cùng một cấu hình:
  JSON
    {
      "project_name": "my_project",
      "python_version": "3.11",
      "debug": true
    }
  YAML
    project_name: my_project
    python_version: "3.11"
    debug: true
  
  TOML
    project_name = "my_project"
    python_version = "3.11"
    debug = true

# TOML đặc biệt phù hợp cho configuration của developer tools, nên bạn sẽ gặp nó rất nhiều trong các Python project hiện đại.
# Trong project bootstrap_project của bạn, mình khuyên nên dùng pyproject.toml ngay từ đầu. Nó sẽ giúp script bootstrap của bạn tạo ra project Python tương đối chuẩn thay vì chỉ tạo folder/file.
# Nếu muốn, bước tiếp theo mình có thể giải thích từng dòng pyproject.toml nên có gì, rồi chúng ta đưa nó vào bootstrap_project của bạn.
```