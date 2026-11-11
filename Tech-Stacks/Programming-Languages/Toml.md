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
File .toml cũng là file dùng để lưu trữ cấu hình (Configuration), tương tự YAML. Tuy nhiên, TOML được thiết kế đặc biệt để con người dễ đọc, dễ chỉnh sửa và phù hợp với cấu hình của các dự án phần mềm.

TOML là viết tắt của Tom's Obvious, Minimal Language.

Bạn sẽ thường gặp file pyproject.toml trong các dự án Python.
1. File TOML dùng để làm gì?
Một số ứng dụng phổ biến:
File	Chức năng
pyproject.toml	Cấu hình dự án Python, dependencies, build system
Cargo.toml	Quản lý dự án và thư viện của Rust
ruff.toml	Cấu hình công cụ kiểm tra code Python
poetry.toml	Cấu hình Poetry
pytest.ini	Lưu ý: đây là INI, không phải TOML

2. Cấu trúc file TOML
Ví dụ file config.toml:
[app]
name = "my_project"
version = "1.0"
debug = true

[database]
host = "localhost"
port = 3306
username = "root"

[model]
name = "gpt-4"
temperature = 0.7
max_tokens = 2000


Giải thích:
- [app]: khai báo một section (nhóm cấu hình).
- name = "my_project": khai báo key-value.
- [database]: nhóm cấu hình database.
- [model]: nhóm cấu hình model AI.
TOML cũng hỗ trợ danh sách:
dependencies = [
    "numpy",
    "pandas",
    "scikit-learn"
]


3. TOML khác YAML và JSON như thế nào?
Cùng một dữ liệu được biểu diễn bằng ba định dạng:
JSON
{
  "app": {
    "name": "my_project",
    "debug": true
  }
}



YAML
app:
  name: my_project
  debug: true



TOML
[app]
name = "my_project"
debug = true



So sánh:
Tiêu chí	JSON	YAML	TOML
Dễ đọc	Khá	Rất tốt	Rất tốt
Cấu trúc	{}	Thụt lề	[section]
Comment	Không	Có #	Có #
Cấu hình dự án	Có	Có	Rất phù hợp
Trao đổi dữ liệu API	Rất phổ biến	Ít phổ biến	Ít phổ biến

4. TOML đặc biệt quan trọng trong Python: pyproject.toml
Đây là phần bạn nên chú ý.

Trong các dự án Python hiện đại, pyproject.toml thường được dùng để quản lý cấu hình dự án và dependencies.

Ví dụ:
[project]
name = "my-ai-agent"
version = "1.0.0"
description = "My AI Agent project"
requires-python = ">=3.11"

dependencies = [
    "langchain",
    "langgraph",
    "playwright",
    "python-dotenv",
    "pyyaml"
]

[tool.ruff]
line-length = 88

[tool.pytest.ini_options]
testpaths = ["tests"]


Ý nghĩa:
- [project]: thông tin dự án Python.
- dependencies: các thư viện cần thiết.
- [tool.ruff]: cấu hình công cụ Ruff.
- [tool.pytest.ini_options]: cấu hình pytest.
Bạn có thể dùng pip install . để cài dự án cùng các dependencies được khai báo trong pyproject.toml (nếu dự án có cấu hình build phù hợp).
5. Đọc file TOML bằng Python
Python 3.11 trở lên đã có sẵn thư viện tomllib, không cần cài thêm.

File config.toml:
[database]
host = "localhost"
port = 3306


Python:
import tomllibwith open("config.toml", "rb") as file:    config = tomllib.load(file)print(config["database"]["host"])print(config["database"]["port"])



Kết quả:
localhost
3306


Lưu ý: tomllib chỉ hỗ trợ đọc TOML, không hỗ trợ ghi file. Muốn ghi có thể dùng thư viện tomli-w.

6. Khi nào nên dùng TOML, YAML, JSON?
TOML
Cấu hình dự án

Ví dụ: pyproject.toml, dependencies, cấu hình công cụ Python.

YAML
Cấu hình hệ thống và workflow

Ví dụ: Docker Compose, GitHub Actions, Kubernetes, cấu hình pipeline.

JSON
Trao đổi dữ liệu

Ví dụ: REST API, dữ liệu gửi/nhận giữa frontend và backend, LLM trả kết quả có cấu trúc.

Lời khuyên: Với các dự án Python AI Agent/LangGraph của bạn, nên hiểu và sử dụng cả ba:
- pyproject.toml: quản lý dự án và thư viện.
- config.yaml: quản lý cấu hình ứng dụng, agent, model.
- JSON: định dạng dữ liệu đầu vào/đầu ra giữa các thành phần.
Chúng không thay thế nhau hoàn toàn mà thường được sử dụng cùng nhau trong một dự án.
Đúng rồi. Cả JSON, YAML và TOML đều có thể dùng để cấu hình dự án. Tuy nhiên, không nên chọn tùy ý mà nên dựa vào loại cấu hình và công cụ mà dự án sử dụng.

Mình đưa ra một quy tắc thực tế để bạn dễ quyết định.
1. Quy tắc chọn định dạng
TOML

Ưu tiên cho Python

Dùng khi cấu hình thông tin dự án, dependencies và công cụ phát triển.

Ví dụ:
- pyproject.toml
- Cấu hình Ruff, pytest, Poetry.


YAML

Ưu tiên cho workflow

Dùng khi cấu hình có nhiều cấp phân nhánh, pipeline hoặc hệ thống triển khai.

Ví dụ:
- docker-compose.yml
- GitHub Actions.
- Kubernetes.
- Cấu hình Agent.


JSON

Ưu tiên cho trao đổi dữ liệu

Dùng khi dữ liệu cần truyền giữa các hệ thống hoặc API.

Ví dụ:
- API request/response.
- LLM output.
- Dữ liệu trao đổi giữa frontend và backend.


2. Nếu làm một dự án Python thực tế thì nên tổ chức thế nào?
Ví dụ bạn xây dựng một AI Agent sử dụng LangGraph, LangChain và Playwright.

Mình đề xuất cấu trúc:
my_project/
│
├── pyproject.toml
├── config.yaml
├── .env
│
├── src/
│   └── app/
│       ├── main.py
│       ├── agent.py
│       └── tools.py
│
├── tests/
│   └── test_agent.py
│
└── data/
    └── input.json


Mỗi file có một nhiệm vụ riêng:
File	Dùng để làm gì?
pyproject.toml	Khai báo dependencies, Python version, cấu hình công cụ
config.yaml	Cấu hình Agent, LLM, Playwright
.env	Lưu API key, mật khẩu, thông tin nhạy cảm
input.json	Lưu hoặc trao đổi dữ liệu JSON

Ví dụ cụ thể:

pyproject.toml
[project]
name = "my-agent"
version = "1.0.0"
requires-python = ">=3.11"

dependencies = [
    "langchain",
    "langgraph",
    "playwright",
    "pyyaml",
    "python-dotenv"
]


config.yaml
llm:
  provider: openai
  model: gpt-4
  temperature: 0.2

browser:
  browser_type: chromium
  headless: false

agent:
  max_iterations: 10
  verbose: true


.env
OPENAI_API_KEY=your_api_key
DATABASE_URL=your_database_url


3. Một số lưu ý quan trọng khi lựa chọn
Có 3 nguyên tắc bạn nên nhớ:

Nguyên tắc 1: Ưu tiên định dạng mà công cụ yêu cầu.

Ví dụ:
- Python project hiện đại sử dụng pyproject.toml.
- Docker Compose hỗ trợ YAML.
- GitHub Actions sử dụng YAML.
Không nên đổi định dạng chỉ vì bạn thích định dạng khác.

Nguyên tắc 2: Không sử dụng quá nhiều định dạng cho cùng một mục đích.

Ví dụ, không cần tạo cả ba file:
config.json
config.yaml
config.toml


chỉ để lưu cùng một cấu hình. Điều này dễ gây trùng lặp và khó bảo trì.

Nguyên tắc 3: Không lưu thông tin bí mật trong file cấu hình thông thường.

API key, password, token nên đưa vào .env hoặc hệ thống quản lý secrets.

4. Kết luận: Nên học cái nào trước?
Nếu bạn phát triển Python Backend, AI Agent, Machine Learning thì mình khuyên thứ tự:
1. TOML: Hiểu cách quản lý dự án Python và dependencies.
2. YAML: Hiểu cách quản lý cấu hình ứng dụng và workflow.
3. JSON: Nắm thật chắc vì rất thường xuyên làm việc với API, LLM và dữ liệu có cấu trúc.
Một điều quan trọng: Trong dự án chuyên nghiệp, bạn không cần cố gắng dùng cả ba. Hãy chọn định dạng phù hợp với từng nhiệm vụ, ưu tiên sự nhất quán và khả năng bảo trì.