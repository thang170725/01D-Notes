File .yml (hoặc .yaml) là file dùng để lưu trữ dữ liệu cấu hình (Configuration). Nó thường được sử dụng để khai báo các thiết lập cho ứng dụng, dự án, Docker, CI/CD, Kubernetes và nhiều công cụ khác.

YAML viết tắt của YAML Ain't Markup Language.
1. File YAML dùng để làm gì?
Một số mục đích phổ biến:
Mục đích	Ví dụ
Cấu hình ứng dụng	config.yml
Quản lý môi trường	environment.yml
Cấu hình Docker	docker-compose.yml
Cấu hình AI/LLM	config.yaml
CI/CD	.github/workflows/main.yml
Kubernetes	deployment.yaml
Cấu hình thư viện Python	mkdocs.yml

2. Ví dụ một file YAML
Giả sử bạn có dự án Python và muốn lưu cấu hình:

config.yml
app:
  name: my_project
  version: 1.0
  debug: true

database:
  host: localhost
  port: 3306
  username: root
  password: 123456

model:
  name: gpt-4
  temperature: 0.7
  max_tokens: 2000


YAML cho phép tổ chức dữ liệu theo cấu trúc phân cấp thông qua thụt lề.

Ví dụ:
database:
  host: localhost
  port: 3306


Ở đây:
- database là một object.
- host và port là các thuộc tính bên trong database.
- localhost là giá trị của host.
- 3306 là giá trị của port.
3. YAML khác JSON như thế nào?
Cùng một dữ liệu nhưng có hai cách biểu diễn:

JSON:
{
  "app": {
    "name": "my_project",
    "debug": true
  }
}


YAML:
app:
  name: my_project
  debug: true


YAML thường dễ đọc và dễ chỉnh sửa hơn vì:
- Không cần dấu {}.
- Không cần dấu ,.
- Không cần dấu ngoặc kép cho phần lớn chuỗi đơn giản.
- Có thể sử dụng comment bằng #.
4. Đọc file YAML bằng Python
Bạn có thể sử dụng thư viện PyYAML.

Cài đặt:
pip install pyyaml


Ví dụ:

config.yml
browser:
  name: chromium
  headless: false

website:
  url: https://youtube.com


main.py
import yamlwith open("config.yml", "r", encoding="utf-8") as file:    config = yaml.safe_load(file)print(config["browser"]["name"])print(config["browser"]["headless"])print(config["website"]["url"])



Kết quả:
chromium
False
https://youtube.com


5. Khi nào nên dùng YAML thay vì viết trực tiếp trong Python?
Ví dụ dự án Playwright của bạn:

Thay vì viết cấu hình trực tiếp:
browser = p.chromium.launch(    headless=False,    slow_mo=500)page.goto("https://youtube.com")



Bạn có thể tách cấu hình ra file YAML:
browser:
  name: chromium
  headless: false
  slow_mo: 500

website:
  url: https://youtube.com


Sau đó Python đọc cấu hình để thực thi.

Lợi ích:
- Thay đổi cấu hình mà không cần sửa code.
- Tách biệt logic chương trình và cấu hình.
- Dễ quản lý nhiều môi trường Development, Testing, Production.
- Dễ chia sẻ cấu hình giữa các thành viên trong nhóm.

Tóm lại: YAML không phải ngôn ngữ lập trình. Nó là định dạng biểu diễn dữ liệu, thường được dùng để cấu hình ứng dụng.

Nếu bạn làm dự án Python, AI Agent, LangGraph hoặc Playwright thì hiểu YAML khá quan trọng vì bạn sẽ thường xuyên gặp các file .yml và .yaml.