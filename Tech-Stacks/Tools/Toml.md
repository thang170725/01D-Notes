Nếu bạn đang làm Python project như bootstrap_project mà mình đang hướng dẫn bạn, thì file .toml thường dùng để cấu hình project.

Nó giống một file .json, .yaml, .ini nhưng có cú pháp riêng, khá dễ đọc.

1. Ví dụ đơn giản

Bạn có thể có:

bootstrap_project/
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

Tên project là gì
Version bao nhiêu
Python tối thiểu là bao nhiêu
Project cần những thư viện nào
2. .toml không chỉ dành cho Python

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

Có thể hiểu:

TOML
 ↓
File cấu hình
 ↓
Chương trình đọc cấu hình này
3. Tại sao Python hay dùng pyproject.toml?

Đây là phần quan trọng với project bootstrap_project của bạn.

Ngày trước Python thường có:

requirements.txt
setup.py
setup.cfg

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

Sau đó các tool như package manager/build tool/linter/formatter có thể đọc cấu hình từ đó.

4. Với project bootstrap của bạn, TOML sẽ rất hữu ích

Ví dụ bạn muốn script tạo project Python theo kiến trúc cố định:

my_project/
├── pyproject.toml
├── README.md
├── .gitignore
├── src/
│   └── my_project/
│       ├── __init__.py
│       ├── core/
│       ├── pipelines/
│       └── utils/
└── tests/

Thì bootstrap_project có thể tự sinh ra pyproject.toml:

[project]
name = "my_project"
version = "0.1.0"
requires-python = ">=3.11"

[tool.pytest.ini_options]
testpaths = ["tests"]

Như vậy mỗi lần bạn chạy:

python bootstrap.py my_project

nó tự tạo cả kiến trúc + cấu hình project.

5. TOML khác JSON/YAML thế nào?

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

TOML đặc biệt phù hợp cho configuration của developer tools, nên bạn sẽ gặp nó rất nhiều trong các Python project hiện đại.

Trong project bootstrap_project của bạn, mình khuyên nên dùng pyproject.toml ngay từ đầu. Nó sẽ giúp script bootstrap của bạn tạo ra project Python tương đối chuẩn thay vì chỉ tạo folder/file.

Nếu muốn, bước tiếp theo mình có thể giải thích từng dòng pyproject.toml nên có gì, rồi chúng ta đưa nó vào bootstrap_project của bạn.