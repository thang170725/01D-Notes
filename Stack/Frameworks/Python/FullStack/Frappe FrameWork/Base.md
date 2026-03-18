- [Vì sao ERP dùng Frappe?](#vì-sao-erp-dùng-frappe)

---
- [root - Bản đồ nhanh (đọc trước)](#root---bản-đồ-nhanh-đọc-trước)
- [apps/](#apps)
  - [frappe/](#frappe)
  - [my-app/](#my-app)
    - [my-app/](#my-app-1)
- [config/ – HẬU TRƯỜNG (SERVICE)](#config--hậu-trường-service)
- [logs/ – HỘP ĐEN](#logs--hộp-đen)
- [Procfile – KỊCH BẢN CHẠY](#procfile--kịch-bản-chạy)
- [patches.txt – LỊCH SỬ CẬP NHẬT](#patchestxt--lịch-sử-cập-nhật)

---
- [Introduction](#introduction)
- [Tạo project \& môi trường ảo python (thư mục làm việc)](#tạo-project--môi-trường-ảo-python-thư-mục-làm-việc)
- [Cập nhật và cài đặt gói hệ thống cốt lõi](#cập-nhật-và-cài-đặt-gói-hệ-thống-cốt-lõi)
- [Thiết lập liên kết python](#thiết-lập-liên-kết-python)
- [Cài đặt MariaDB và cấu hình frappe \& khởi động lại mariadb](#cài-đặt-mariadb-và-cấu-hình-frappe--khởi-động-lại-mariadb)
- [Cài đặt node.js và yarn](#cài-đặt-nodejs-và-yarn)
- [Cài đặt Frappe Bench CLI](#cài-đặt-frappe-bench-cli)
- [Tạo thư mục cha](#tạo-thư-mục-cha)
- [Khởi tạo bench.](#khởi-tạo-bench)
- [Tạo site mới](#tạo-site-mới)
- [Sửa file hosts](#sửa-file-hosts)
- [Chạy frappe bench](#chạy-frappe-bench)
- [Tạo App (mã nguồn)](#tạo-app-mã-nguồn)
- [Cài app vào site](#cài-app-vào-site)
- [Build Assets và đồng bộ database](#build-assets-và-đồng-bộ-database)
- [Kích hoạt developer mode](#kích-hoạt-developer-mode)
- [vào site cụ thể](#vào-site-cụ-thể)
- [exit()](#exit)
- [.new\_doc() \& .title](#new_doc--title)
- [update data](#update-data)
- [.get\_last\_doc()](#get_last_doc)
- [get\_all](#get_all)
- [get\_list](#get_list)
- [delete\_doc()](#delete_doc)
- [Tạo Doctype (bắt buộc)](#tạo-doctype-bắt-buộc)
- [Frontend structure (chuẩn crm)](#frontend-structure-chuẩn-crm)
- [FETCH LIST (KHÔNG VIẾT BACKEND)](#fetch-list-không-viết-backend)
- [Bản đồ nhanh](#bản-đồ-nhanh)
- [site\_config.json – NÃO CỦA SITE (QUAN TRỌNG NHẤT)](#site_configjson--não-của-site-quan-trọng-nhất)
- [private/ – KHO KÍN (USER KHÔNG XEM ĐƯỢC)](#private--kho-kín-user-không-xem-được)
- [public/ – KHO MỞ (AI CŨNG XEM ĐƯỢC 😄)](#public--kho-mở-ai-cũng-xem-được-)
- [frappe.msgprint](#frappemsgprint)
- [frappe.throw](#frappethrow)
- [Ví dụ về site](#ví-dụ-về-site)
- [Commit()](#commit)
- [Rollback()](#rollback)
- [.as\_dict()](#as_dict)
- [.get\_meta \& .fields](#get_meta--fields)
  - [.has\_field()](#has_field)
- [Cài Vue](#cài-vue)
- [Vào site\_config ở site](#vào-site_config-ở-site)
- [Cách 2](#cách-2)
- [root - Bản đồ nhanh (đọc trước)](#root---bản-đồ-nhanh-đọc-trước)
- [apps/](#apps)
  - [frappe/](#frappe)
  - [my-app/](#my-app)
    - [my-app/](#my-app-1)
- [config/ – HẬU TRƯỜNG (SERVICE)](#config--hậu-trường-service)
- [logs/ – HỘP ĐEN](#logs--hộp-đen)
- [Procfile – KỊCH BẢN CHẠY](#procfile--kịch-bản-chạy)
- [patches.txt – LỊCH SỬ CẬP NHẬT](#patchestxt--lịch-sử-cập-nhật)
- [Vì sao ERP dùng Frappe?](#vì-sao-erp-dùng-frappe)

---
# Introduction
```bash
- Frappe Framework là một web framework full-stack dùng để xây dựng:
  + ERP
  + CRM
  + hệ thống quản lý nội bộ
  + dashboard dữ liệu
  + web app doanh nghiệp
- Framework này nổi tiếng vì là nền tảng để xây dựng ERPNext – một hệ thống ERP mã nguồn mở rất phổ biến.
- Tech stack chính của Frappe:
  + Backend	    : Python
  + Database	  : MariaDB
  + Frontend	  : JavaScript
  + API	        : REST
  + Realtime	  : WebSocket
  + Task queue  : Redis
```
# Tạo project & môi trường ảo python (thư mục làm việc)
```bash
1. mkdir ~/frappe-vue-test
2. cd ~/frappe-vue-test
3. python3.10 -m venv .venv  : Tạo virtual environment với Python 3.10
4. source .venv/bin/activate
```
**Kiểm tra**
```bash
which python
python --version
pip --version
```

# Cập nhật và cài đặt gói hệ thống cốt lõi
```bash
sudo apt update             : cập nhật danh sách phần mềm.
sudo apt install -y         : cài hàng loạt phần mềm 1 lần
    git \                   : dùng để tải source code, frappe được clone từ gitHub
    build-essential \       : bộ công cụ biên dịch C/C++
    curl \                  : tải file từ internet bằng dòng lệnh. Frappe / Bench dùng curl để: tải script, tải Node, tải tool phụ
    python3-dev \           : Cho phép Python build thư viện “có lõi C”
    python3-pip \           : Trình cài thư viện Python
    python3-venv \          : Tạo môi trường ảo
    redis-server \          : Bộ nhớ nhanh (cache + queue). Frappe dùng Redis cho: cache background job, task async
                              Ví dụ: gửi email, xử lý dữ liệu nền, crawl / sync. Không có Redis → Frappe không khởi động
    libmariadb-dev \        : Thư viện cho Python nói chuyện với MariaDB, Khi bạn cài: pip install mysqlclient Nó cần: header 
                              file lib mariadb. Thiếu → không kết nối DB được
    mariadb-server \        : Database server
    mariadb-client \        : Tool kết nối & quản lý DB
    pkg-config              : Trợ lý cho compiler. Nó giúp: tìm thư viện hệ thống, tìm đúng version, link đúng file Không dùng trực 
                              tiếp, nhưng: thiếu → build lib dễ fail
sudo apt update
sudo apt install -y \
    git \
    build-essential \
    curl \
    python3-dev \
    python3-pip \
    python3-venv \
    redis-server \
    libmariadb-dev \
    mariadb-server \
    mariadb-client \
    pkg-config

```

# Thiết lập liên kết python
```bash
# Gói này sẽ giúp lệnh 'python' gọi đến 'python3'
sudo apt install -y python-is-python3
```

# Cài đặt MariaDB và cấu hình frappe & khởi động lại mariadb
```bash
sudo systemctl start mariadb    : bật MariaDB lên để nó chạy
sudo mysql_secure_installation  : khóa & dọn dẹp MariaDB cho an toàn
```
**Kiểm tra nhanh DB có chạy không**
```bash
systemctl status mariadb
```
**tùy chọn**
```text
Cấu hình MariaDB cho Frappe: Mở file cấu hình database (thường là /etc/mysql/mariadb.conf.d/50-server.cnf) và thêm/chỉnh sửa các cài đặt sau vào phần [mysqld] để đảm bảo hỗ trợ UTF-8mb4 và chế độ nghiêm ngặt:
```
```bash
Ini, TOML
[mysqld]
# Thiết lập bộ ký tự
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

# Thiết lập chế độ nghiêm ngặt (Strict Mode)
sql-mode="STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION"

[mysql]
default-character-set = utf8mb4

```
**Cuối cùng**

```bash
sudo systemctl restart mariadb  : Khởi động lại MariaDB
```

# Cài đặt node.js và yarn
```bash
curl -sL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs
sudo npm install -g yarn
```

# Cài đặt Frappe Bench CLI
```bash
pip3 install frappe-bench
```

# Tạo thư mục cha
```bash
mkdir fw
cd fw
```

# Khởi tạo bench. 
Lệnh này sẽ tải Frappe Framework về và tạo thư mục 'frappe-bench'
```bash
bench init frappe-bench \
  --frappe-branch version-15 \
  --python /usr/bin/python3.11
cd frappe-bench
```

# Tạo site mới
```bash
bench new-site dev.local
```
**Tại sao phải tạo site mới**
```text
- Site = 1 hệ thống độc lập hoàn chỉnh. Không có site → Frappe không chạy được. Bạn KHÔNG thao tác trực tiếp trên Frappe core.
- Ví dụ đời thường (quan trọng nhất) Frappe giống gì?
    + Frappe = Windows / Android
    + Site = từng máy tính / từng điện thoại
    + Bạn không: mở Windows rồi lưu dữ liệu chung cho tất cả máy mà mỗi máy có user, app, dữ liệu riêng
- Nếu không có site thì chuyện gì xảy ra? Giả sử KHÔNG có site:
    + User A
    + User B
    + Công ty X
    + Công ty Y
    -> Tất cả: chung DB, chung config, chung quyền -> toang toàn bộ
- Site thực chất chứa những gì? Mỗi site có:
    + 1 database riêng
    + user riêng
    + quyền riêng
    + config riêng
    + dữ liệu riêng Nằm ở: sites/dev.local/
```
**Vì sao Frappe bắt buộc phải có site?**
```text
- Vì Frappe: là framework đa tenant
- thiết kế để:
    + 1 code
    + nhiều hệ thống
- Không tạo site thì:
    + không có DB
    + không có user
    + không có config
    + không có dữ liệu
```
**Ví dụ**
```text
- Bạn làm dự án BĐS + AI. Bạn muốn:
    + dev thử nghiệm
    + test crawl
    + prod chạy thật
- Bạn tạo:
    + dev.local
    + test.local
    + prod.domain.com
    + Mỗi site:
        + DB riêng
        + data riêng
        + không đụng nhau
```

# Sửa file hosts
```bash
sudo nano /etc/hosts
di chuyển con trỏ xuống cuối
gõ: 127.0.0.1   dev.local
Bấm theo đúng thứ tự:
1. CTRL + S
3. CTRL + X (Exit)
-> Xong, nano sẽ tự thoát.
```
Hoặc
```bash
bench --site dev.local add-to-hosts
```
**Kiểm tra**
```bash
ping dev.local
nếu thây: PING dev.local (127.0.0.1) -> OK
```

# Chạy frappe bench
```bash
cd ~/workspace/thang-dev/fw/frappe-bench
bench start
Mở trình duyệt: http://dev.local:8000 hoặc http://dev.local:8000/desk
```
**Login**
```bash
Username: Administrator
Password: (mật khẩu bạn nhập lúc tạo site)
```
**Quên mật khẩu**
```bash
bench --site dev.local set-admin-password
```

# Tạo App (mã nguồn)
**Điều kiện**
```bash
cd ~/workspace/thang-dev/fw/frappe-bench
ls
Phải thấy: apps  sites  env  Procfile ...
```
**Chạy lệnh tạo app**
```bash
bench new-app my_custom_hr_app
```

# Cài app vào site
Tạo app xong chưa chạy được. Phải gắn nó vào site dev.local
```bash
bench --site dev.local install-app my_custom_hr_app
```
**Kiểm tra**
```bash
bench --site dev.local list-apps hoặc Mở giao diện: Settings → Apps
```

# Build Assets và đồng bộ database
```bash
bench build
bench --site dev.local migrate
bench start
```

# Kích hoạt developer mode
```text
- Developer Mode = chế độ dành cho người làm ứng dụng, không phải người chỉ sử dụng hệ thống.
- Khi bật Developer Mode, Frappe coi mọi thứ bạn tạo (DocType, Report, Web Form,…) là MÃ NGUỒN, chứ không chỉ là dữ liệu trong database.
- Nhờ đó:
    + Có file .json, .py, .js thật sự
    + Có thể dùng Git
    + Có thể deploy, backup, code review
    + Có thể viết logic tùy biến
```
**Không bật Developer Mode thì chuyện gì xảy ra?**
**Giả sử KHÔNG bật developer_mode mà bạn tạo DocType Article**
```text
- Điều xảy ra:
  + DocType chỉ được lưu trong database
  + KHÔNG có file article.json, article.py, article.js
  + Git không biết gì để commit
  + Sang server khác → mất DocType
  + Không viết được logic backend/frontend chuẩn chỉnh
- Trường hợp này phù hợp cho:
  + Người dùng cuối
  + Admin chỉ cấu hình ERP
  + KHÔNG phù hợp cho dev
```
**Vì sao Frappe “ép” bật Developer Mode khi làm app?**
- Frappe được thiết kế theo triết lý:
  + Everything is Metadata + Code
DocType không chỉ là bảng DB, mà là:
  + Model
  + View
  + Controller
  + Permission
  + Workflow
  + Validation
- Nên Frappe cần export định nghĩa DocType ra file để:
  + Theo dõi thay đổi
  + Đồng bộ giữa các site
  + Deploy CI/CD
  + Rollback khi lỗi
  + Tất cả việc đó chỉ làm được khi bật Developer Mode.
**Developer Mode đã làm gì “dưới mui xe”?**
```text
- Khi bạn bật:
  + bench set-config -g developer_mode true
- Frappe thay đổi hành vi như sau:
  + Trước (developer_mode = false)
  + DocType → DB
  + Custom Field → DB
  + Script → DB
  + Sau (developer_mode = true)
  + DocType → article.json
  + Logic server → article.py
  + Logic client → article.js
  + Test → test_article.py
DB chỉ là runtime, còn source of truth là code.
```
- [vào site cụ thể](#vào-site-cụ-thể)
- [exit()](#exit)
- [.new\_doc() \& .title](#new_doc--title)
- [update data](#update-data)
- [.get\_last\_doc()](#get_last_doc)
- [get\_all](#get_all)
- [get\_list](#get_list)
- [delete\_doc()](#delete_doc)
- [Commit()](#commit)
- [Rollback()](#rollback)
- [.as\_dict()](#as_dict)
- [.get\_meta \& .fields](#get_meta--fields)
  - [.has\_field()](#has_field)

---

# vào site cụ thể
```bash
bench --site dev.local console
```

# exit()
Thoát.

# .new_doc() & .title
```bash
doc = frappe.new_doc('')
Cách tạo ra một doctype mới.

# frappe.get_doc() & .insert() & .save()
Tạo document hoặc lấy document theo name.
**Ex: Tạo document**
```bash
doc = frappe.get_doc({
    "doctype": "Article",
    "article_name": "Clean Code",
    "isbn": "1234567890",
    "status": "Available"
})
doc.insert()
```
**Ex: Lấy document theo name**
```bash
doc = frappe.get_doc("Article", "My First Book")
- Lấy một document article có name="My First Book"" từ database.
```
# update data
Thay đổi dữ liệu.
**Ex**
```bash
doc.status = "Issued" // status là tên cột của bảng
doc.save()
```

3️⃣ Query dữ liệu (rất hay dùng)
🔹 frappe.db.exists
frappe.db.exists("Article", "Clean Code")

# .get_last_doc()
```bash
doc = frappe.get_last_doc(
    doctype, 
    filters={'status': 'Cancelled'},    # status là field, Cacelled là giá trị cụ thể của field
    order_by)
```
**Ex**
```bash
doc = frappe.get_last_doc('Article')
```

# get_all
```bash
frappe.get_all(
    "Article",
    filters={"status": "Available"},
    fields=["name", "author"]
)
```

# get_list
Lấy ra danh sách data.
**Ex**
```bash
frappe.get_list(
    "Article",
    filters={"status": "Available"},
    fields=["name", "publisher"],
    limit_page_length=5

-- SQL thuần --
frappe.db.sql("""
    SELECT name, status
    FROM `tabArticle`
    WHERE status = 'Available'
""", as_dict=True)
)
```
# delete_doc()
```bash
frappe.delete_doc(
    doctype='Article',
    name='My Third Book',
    force=True              # nếu muốn bỏ qua permission
```
**Ex**
```bash
frappe.delete_doc("Article", "Clean Code") # Clean Code là name trong doctype đó
```

4️⃣ Test validate / hook / msgprint
🔹 Test frappe.throw
doc = frappe.get_doc({
    "doctype": "Article",
    "article_name": "Bad ISBN",
    "isbn": "123",
    "status": "Available"
})
doc.insert()   # ❌ ValidationError

🔹 Test frappe.msgprint
frappe.clear_messages()

doc = frappe.get_doc({
    "doctype": "Article",
    "article_name": "No Publisher",
    "isbn": "1234567890",
    "status": "Available"
})
doc.insert()

frappe.get_messages()

5️⃣ Gọi API (@frappe.whitelist)
frappe.call(
    "book.book.doctype.article.article.my_api",
    arg1="hello"
)


Hoặc

from book.book.doctype.article.article import my_api
my_api("hello")

6️⃣ Quyền & user
🔹 Đổi user
frappe.set_user("Administrator")

frappe.set_user("test@example.com")

🔹 Bỏ qua permission (debug)
doc.insert(ignore_permissions=True)

7️⃣ Commit / Rollback DB

📌 
```bash
CRM frontend KHÔNG tự query DB → nó luôn đi theo 3 tầng:
Doctype (schema)
   ↓
API chuẩn của Frappe (reportview / client / CRM api)
   ↓
frappe-ui (createResource / ListView / Modal)

- KHÔNG viết backend mới nếu chưa cần
- 90% CRUD dùng API có sẵn
```

# Tạo Doctype (bắt buộc)
**Ở đâu**
```bash
CRM > Developer > DocType
```
**Ex**
```bash
Simple Item
- title (Data, reqd)
- description (Small Text)
- quantity (Int)
- status (Select: Draft\nActive\nInactive)

- Check:
    + Is Submittable ❌
    + Is Tree ❌
    + Allow Rename ❌

XONG → DB có bảng
```

# Frontend structure (chuẩn crm)
frontend/src/pages/simple-item/
```bash
simple-item/
├─ SimpleItemList.vue        (page)
├─ SimpleItemListView.vue    (component | list + bulk actions)
├─ SimpleItemModal.vue       (component |create / edit)

- CRM luôn tách như vậy
    + Page = orchestration
    + ListView = table + bulk
    + Modal = form
```

# FETCH LIST (KHÔNG VIẾT BACKEND)
Ở file page (SimpleItemList.vue)
```bash
const items = createResource({
  url: 'frappe.desk.reportview.get',
  params: {
    doctype: 'Simple Item',
    fields: ['name', 'title', 'description', 'quantity', 'status'],
    order_by: 'modified desc',
    limit_page_length: 50,
  },
  auto: true,
})
```
Dữ liệu trả về
```bash
values = [
  ['ID1', 'Title 1', 'Desc', 2, 'Draft'],
  ...

CRM dùng cách này 100%
]

# MAP → ROWS (FORMAT CHO LISTVIEW)
const rows = computed(() =>
  items.data?.values.map((r) => ({
    name: r[0],
    title: { label: r[1] },
    description: { label: r[2] },
    quantity: { label: r[3] },
    status: { label: r[4] },
  })) || []
)


⚠️ BẮT BUỘC

mỗi cell = { label: value }

name phải tồn tại

HIỂN THỊ LIST (GIỐNG CRM)

📍 SimpleItemListView.vue

<ListView
  :rows="rows"
  :columns="columns"
  row-key="name"
  :options="{ selectable: true }"
>
  <ListRows :rows="rows" />

  <ListSelectBanner>
    <template #actions="{ selections, unselectAll }">
      <Dropdown :options="bulkActions(selections, unselectAll)">
        <Button icon="more-horizontal" variant="ghost" />
      </Dropdown>
    </template>
  </ListSelectBanner>
</ListView>

BULK ACTIONS (EDIT / DELETE)
function bulkActions(selections, unselectAll) {
  return [
    {
      label: 'Edit',
      disabled: selections.length !== 1,
      onClick: () => {
        emit('edit', selections[0].name)
        unselectAll()
      },
    },
    {
      label: 'Delete',
      destructive: true,
      onClick: async () => {
        for (const r of selections) {
          await call('frappe.client.delete', {
            doctype: 'Simple Item',
            name: r.name,
          })
        }
        emit('reload')
        unselectAll()
      },
    },
  ]
}


✔️ Giống CRM Task / Lead 100%

CREATE / EDIT MODAL (DÙNG API CHUẨN)

📍 SimpleItemModal.vue

➕ Create
call('frappe.client.insert', {
  doc: {
    doctype: 'Simple Item',
    ...form.value,
  },
})

✏️ Edit
call('frappe.client.set_value', {
  doctype: 'Simple Item',
  name: form.value.name,
  fieldname: {
    title: form.value.title,
    description: form.value.description,
    quantity: form.value.quantity,
    status: form.value.status,
  },
})

- [Bản đồ nhanh](#bản-đồ-nhanh)
- [site\_config.json – NÃO CỦA SITE (QUAN TRỌNG NHẤT)](#site_configjson--não-của-site-quan-trọng-nhất)
- [private/ – KHO KÍN (USER KHÔNG XEM ĐƯỢC)](#private--kho-kín-user-không-xem-được)
- [public/ – KHO MỞ (AI CŨNG XEM ĐƯỢC 😄)](#public--kho-mở-ai-cũng-xem-được-)
- [Ví dụ về site](#ví-dụ-về-site)

---

```text
- Thư mục site = “nhà riêng” của 1 hệ thống Frappe
- Mỗi site:
    + có DB riêng
    + có log riêng
    + có file riêng
    + có config riêng
```

# Bản đồ nhanh
```bash
dev.local/
├── site_config.json   → NÃO (cấu hình)
├── private/           → KHO KÍN
├── public/            → KHO MỞ
├── logs/              → NHẬT KÝ
├── locks/             → KHÓA CỬA
```

# site_config.json – NÃO CỦA SITE (QUAN TRỌNG NHẤT)
```bash
{
  "db_name": "_a1b2c3",
  "db_password": "******",
  "db_type": "mariadb"
}

Chứa:
- tên database
- mật khẩu DB
- redis
- socket
- secret key
- Khi Frappe nhận request:
URL → xác định site → đọc site_config.json → connect DB
KHÔNG commit file này lên Git
```

# private/ – KHO KÍN (USER KHÔNG XEM ĐƯỢC)
```bash
private/
├── backups
└── files
```
**private/backups**
```text
- Nơi Frappe:
  + ump DB
  + backup file
  + Lệnh: bench --site dev.local backup
```
**private/files**
File upload KHÔNG public
  + hợp đồng
  + CMND
  + file nhạy cảm
Không truy cập bằng URL

# public/ – KHO MỞ (AI CŨNG XEM ĐƯỢC 😄)
```bash
public/
└── files

File upload công khai
- ảnh
- brochure
- tài liệu marketing
- Truy cập qua: https://dev.local/files/abc.png
```

4️⃣ logs/ – NHẬT KÝ RIÊNG CỦA SITE
logs/
├── database.log
└── database.log.1


👉 Log liên quan:

DB query

lỗi migration

lỗi permission

📌 Debug lỗi site → vào đây

5️⃣ locks/ – Ổ KHÓA (CHỐNG LOẠN)
locks/
└── bench_new_site.lock

DOCUMENT LÀ GÌ?
Nói 1 câu:

Document = 1 instance (1 dòng dữ liệu) của DocType

Ví dụ:

DocType: Article
Bạn bấm New và nhập:

Article Name: AI là gì

Author: Thắng

Status: Available

👉 Cái bạn vừa lưu = 1 Document

Nếu bạn tạo 100 bài viết →
100 Document cùng chung 1 DocType

2️⃣ DOC TYPE vs DOCUMENT (PHẢI PHÂN BIỆT RÕ)
DocType	Document
Bản thiết kế	Dữ liệu thật
Tạo 1 lần	Tạo nhiều lần
Dev định nghĩa	User sử dụng
Giống class	Giống object

👉 Không phân biệt được cái này → học Frappe rất mệt

3️⃣ CRUD TRONG FRAPPE DIỄN RA Ở ĐÂU?
C = Create

Bấm New

Lưu form

R = Read

Article List

Mở 1 Article

U = Update

Edit

Save

D = Delete

Delete (nếu có quyền)

👉 Không cần code → Frappe lo hết

4️⃣ NAME – THỨ KHIẾN NHIỀU NGƯỜI RỐI
name là gì?

Là Primary Key

Không nhất thiết là “tên hiển thị”

Ví dụ:

name = ART-0001
article_name = AI là gì


👉 name = máy dùng
👉 article_name = người dùng nhìn

5️⃣ DOCSTATUS – VÒNG ĐỜI DOCUMENT

Mỗi Document luôn có:

docstatus = 0 | 1 | 2

Giá trị	Ý nghĩa	Sửa được?
0	Draft	✅
1	Submitted	❌
2	Cancelled	❌

👉 DocType thường → chỉ Draft
👉 DocType giao dịch → có Submit
```text
Trong Frappe Framework, frappe.msgprint và frappe.throw đều dùng để hiển thị thông báo cho người dùng, nhưng mục đích và hành vi khác nhau. 
```

# frappe.msgprint 
- Hiển thị thông báo (KHÔNG dừng chương trình)
- Dùng khi nào?
    + Thông báo thành công
    + Nhắc nhở
    + Debug nhanh
    + Không làm gián đoạn xử lý

**Syn**
```bash
frappe.msgprint("Nội dung thông báo")
```
```python
import frappe
from frappe.model.document import Document

class Article(Document):

    def validate(self):
        self.validate_isbn()
        self.warn_if_no_publisher()

    def validate_isbn(self):
        if self.isbn and len(self.isbn) < 10:
            frappe.throw("ISBN phải có ít nhất 10 ký tự")

    def warn_if_no_publisher(self):
        if not self.publisher:
            frappe.msgprint(
                msg="Bạn chưa nhập Publisher",
                title="Cảnh báo",
                indicator="orange"
            )
```
PERMISSION (PHÂN QUYỀN) TRONG FRAPPE

Không code. Không lý thuyết hàn lâm.
Chỉ hiểu vì sao ERP sống được là nhờ cái này.

1️⃣ PERMISSION LÀ GÌ? (NÓI 1 CÂU)

Permission = ai được làm gì với Document nào

2️⃣ VÌ SAO PHẢI CÓ PERMISSION?

Ví dụ đời thật:

Người	Có được làm gì?
Nhân viên	Tạo đơn
Quản lý	Duyệt
Kế toán	Xem
Người lạ	Không thấy

👉 Nếu ai cũng sửa được → ERP vô nghĩa.

3️⃣ 3 THỨ CỐT LÕI TRONG PERMISSION
🧩 1. User (Người dùng)

Email login

Có thể có nhiều Role

🧩 2. Role (Vai trò)

Ví dụ:

Librarian

Library Member

System Manager

👉 Role = cái mũ đội trên đầu

🧩 3. Permission Rule

Quy định:

Role nào

Được làm gì (Read / Write / Create / Delete / Submit)

4️⃣ PERMISSION GẮN Ở ĐÂU?

👉 Gắn vào DocType, không gắn vào User.

DocType Article
 ├─ Librarian → full quyền
 └─ Member → chỉ Read


User chỉ việc:

User → có Role → hưởng quyền

5️⃣ CÁC QUYỀN CƠ BẢN (RẤT QUAN TRỌNG)
Quyền	Ý nghĩa
Read	Xem
Write	Sửa
Create	Tạo
Delete	Xóa
Submit	Submit
Cancel	Cancel
Amend	Tạo bản sửa

👉 Không có quyền → nút biến mất

6️⃣ FRAPPE KIỂM TRA PERMISSION KHI NÀO?

Luôn luôn:

Mở List

Mở Form

Save

Submit

Gọi API

👉 Không có chuyện lách UI

7️⃣ THỰC HÀNH NHẸ (RẤT QUAN TRỌNG)
🎯 Mục tiêu

Cảm nhận Permission bằng mắt

BƯỚC 1: Tạo Role

Awesomebar → Role List

New → Article Viewer

BƯỚC 2: Gán Permission cho DocType Article

Mở DocType Article

Phần Permissions

Thêm dòng:

Role: Article Viewer

Tick: Read

Bỏ hết cái khác

Save

BƯỚC 3: Tạo User test

Awesomebar → User List

New User

Gán Role: Article Viewer

Lưu

BƯỚC 4: Login user đó

👉 Bạn sẽ thấy:

Chỉ xem được Article

Không tạo

Không sửa

8️⃣ ĐIỀU CỰC KỲ QUAN TRỌNG

Permission trong Frappe không phải trang trí UI
Nó là security thật

Backend cũng tuân theo rule này.

9️⃣ TÓM TẮT ĐẾN GIỜ

Bạn đã nắm:

DocType = bản thiết kế

Document = dữ liệu thật

Permission = luật chơi

👉 Đây là 3 trụ cột của Frappe.

🔜 PHẦN TIẾP THEO (BẮT ĐẦU THÚ VỊ)
👉 FORM BEHAVIOR (HÀNH VI FORM)

Vì sao đổi Status → field khác bị khóa?

Vì sao có field chỉ đọc?

Logic UI đến từ đâu?

Không code trước, chỉ hiểu.
# frappe.throw 
```text
- Ném lỗi (DỪNG chương trình ngay)
- Dùng khi nào?
    + Validate dữ liệu
    + Ngăn không cho lưu
    + Trả lỗi về frontend (HTTP 417 / 400)
```
**Syn**
```bash
frappe.throw("Nội dung lỗi")
```
```python
import frappe
from frappe.model.document import Document

class Article(Document):

    def validate(self):
        # validate trước khi lưu (insert & update)
        self.validate_isbn()
        self.validate_status()

    def validate_isbn(self):
        if self.isbn and len(self.isbn) < 10:
            frappe.throw("ISBN phải có ít nhất 10 ký tự")

    def validate_status(self):
        if self.status not in ["Issued", "Available"]:
            frappe.throw("Status không hợp lệ")
```
6️⃣ BÀI THỰC HÀNH NHỎ (KHÔNG CODE)
🎯 Mục tiêu

Cảm nhận Document bằng tay

Làm:

Vào Article List

Bấm New

Tạo 2 Article khác nhau

Quay lại List

👉 Quan sát:

Cùng DocType

Nhiều Document

7️⃣ VẬY BƯỚC TIẾP THEO LOGIC LÀ GÌ?

Bạn đã có:

DocType (bản thiết kế)

Document (dữ liệu)

👉 Câu hỏi tiếp theo tự nhiên là:

“Ai được tạo / sửa / xem Document này?”
👉 Dùng để:

tránh 2 process đụng nhau

tránh chạy migration trùng

📌 Bạn KHÔNG BAO GIỜ đụng vào

6️⃣ Cái gì KHÔNG thấy nhưng RẤT quan trọng?

👉 Database

DB không nằm trong thư mục

nhưng site_config.json trỏ tới DB

📌 Xóa thư mục site ≠ xóa DB (trừ khi bench làm)

# Ví dụ về site
2️⃣ Sites (mỗi site = 1 instance)

Giả sử bạn có 3 khách hàng:

Site	DB	Mục đích
acme.taskmgmt.local	db_acme	Công ty ACME dùng để quản lý công việc thực tế
beta.taskmgmt.local	db_beta	Công ty Beta dùng để test / thử nghiệm
dev.taskmgmt.local	db_dev	Dùng để phát triển, thử feature mới

Sơ đồ:

task_mgmt_bench/
 ├── apps/
 └── sites/
     ├── acme.taskmgmt.local  -> db_acme
     ├── beta.taskmgmt.local  -> db_beta
     └── dev.taskmgmt.local   -> db_dev

3️⃣ Tại sao mỗi site cần DB riêng

ACME có dữ liệu thật của nhân viên, project, task → phải cách ly

Beta chỉ để test → dữ liệu khác

Dev để lập trình → dữ liệu fake, không ảnh hưởng production

Nếu tất cả dùng chung 1 DB thì:

Dữ liệu test và production lẫn lộn → dễ phá hỏng dữ liệu thật

Không thể rollback hoặc restore riêng từng môi trường

4️⃣ Ví dụ chi tiết về workflow

Dev team thêm 1 feature “Giao task tự động cho team member”.

Feature deploy trên dev.taskmgmt.local → dữ liệu dev riêng

QA test trên beta.taskmgmt.local → dữ liệu test riêng

Sau khi ok → deploy cho acme.taskmgmt.local → dữ liệu production an toàn

5️⃣ Tóm tắt
Khái niệm	Trong dự án quản lý công việc
Bench	task_mgmt_bench chứa code chung
Apps	tasks_app, users_app, notifications_app
Site	acme.taskmgmt.local, beta.taskmgmt.local, dev.taskmgmt.local
DB	db_acme, db_beta, db_dev

✅ Kết luận: Bench = code, Site = instance + DB
❌ Không viết whitelist
❌ Không get_doc
✔️ CRM dùng cách này

FLOW DỮ LIỆU (CỰC QUAN TRỌNG)
List page load
   ↓
reportview.get
   ↓
rows[]
   ↓
ListView render
   ↓
User select checkbox
   ↓
ListSelectBanner
   ↓
Edit → emit(name)
   ↓
Page set currentItem
   ↓
Modal open
   ↓
Save → insert / set_value
   ↓
emit('saved')
   ↓
items.reload()
# Commit()
Trong console KHÔNG auto commit.
```bash
frappe.db.commit()
```

# Rollback()
```bash
frappe.db.rollback()
```
8️⃣ Debug nhanh
🔹 In ra log
frappe.log_error("Something wrong", "Article Debug")

# .as_dict()
```bash
print(doc.as_dict())
```
# .get_meta & .fields
Xem field của DocType.
```bash
frappe.get_meta("Article").fields
```

## .has_field()
Kiểm tra field tồn tại.
```bash
frappe.get_meta("Article").has_field("isbn")
```
🔟 Tiện ích hay dùng
frappe.now()
frappe.session.user
frappe.local.site
```bash
bench set-config -g developer_mode true
```

# Cài Vue
```bash
cd apps/todo
npx degit netchampfaris/frappe-ui-starter frontend
cd frontend
yarn
yarn dev
```

# Vào site_config ở site
paste nội dung này vào.
```bash
"allow_cors": "*",
 "ignore_csrf": 1
```

# Cách 2
```bash
1. mkdir dev & cd dev
2. python3.12 -m venv .venv
3. source .venv/bin/activate
4. bench init frappe-bench-15 --frappe-branch version-15 --python /usr/bin/python3.12
5. cd frappe-bench-15/
6. bench new-site mbw15.ts
7. bench use mbw15.ts
8. bench set-config -g developer_mode 1
9. bench get-app erpnext https://github.com/frappe/erpnext --branch version-15
10. bench install-app erpnext
11. bench start (lỗi)
```
# root - Bản đồ nhanh (đọc trước)
```bash
frappe-bench/
├── apps        → CODE (logic)
├── sites       → DATA (dữ liệu + cấu hình site)
├── env         → PYTHON (môi trường)
├── config      → SERVICE (redis, process)
├── logs        → LOG (nhật ký)
├── scripts
├── patches.txt
├── procfile
```

# apps/
```bash
Não bộ (code). Toàn bộ source code của framework Frappe nằm ở đây
- Backend Python
- API
- ORM
- Permission
- Workflow
- UI core
```
**tree**
```bash
apps/
└── frappe/
└── my_custom_hr_app    → App mới do dev tự cài vào

- Không sửa code trong frappe trừ khi bạn biết rõ
```

## frappe/
```bash
- Đây là Frappe Framework source code gốc.
- Nó chứa:
    + ORM
    + Doctype engine
    + Permission
    + API
    + UI backend
    + Toàn bộ xương sống của frappe
- frappe = 1 app nhưng là app nền tảng.
# sites/
Dữ liệu + cấu hình.
```bash
sites/
├── apps.json                   → Danh sách app được enable. Frappe đọc file này để biết: site này dùng app nào. Thiếu → site không 
                                  load app
├── apps.txt                      
├── assets/                     → File tĩnh đã build: JS, CSS, Image. Được sinh ra từ: bench build. Không chỉnh tay
├── dev.local                   
└── common_site_config.json     → Cấu hình dùng chung cho tất cả site Ví dụ: DB host, Redis URL, Socket IO, Background worker. Khi 
                                  Frappe start → đọc file này đầu tiên

- Đây là nơi Frappe sống thực sự
```

## my-app/
```bash
my-app/
├── .git/                   → Quản lý source code (lưu lịch sử commit, branch, diff) → không xóa
├── .gitinore               → Nói với git không track, rất quan trọng khi làm team                      
├── READ.md                 → Mô tả app làm cái gì, cách cài, cách chạy -> không ảnh hưởng runtime, nên viết cho team tương lại
├── license.txt             → bản quyền, bắt buộc nếu open-source    
├── .eslintrc               → check js, chỉ dùng khi bạn viết JS/Frontend              
└── editorconfig            → chuẩn format code, không ảnh hưởng khi chạy, chỉ ảnh hưởng cách viết code
```
### my-app/
```bash
- DocType = bản thiết kế (form + dữ liệu + luật) cho 1 loại giấy tờ.
- Ví dụ đời thực (rất quan trọng): Một tờ “Đơn xin nghỉ phép”
    + Luôn có: Tên người xin, Ngày nghỉ, Lý do, Trạng thái (chờ duyệt / đã duyệt)
    + Trong Frappe: Đơn xin nghỉ phép = 1 DocType. Mỗi lần bạn tạo đơn → đó là 1 Document
```
**Ex**
```bash
DocType: Leave Application
Document: Đơn xin nghỉ của Thắng ngày 10/1
```
**Bên trong 1 DocType có những gì?**
```bash
1. Fields (Trường): Ví dụ: Tên bài viết
    - Ảnh
    - Tác giả
    - Trạng thái
    - Giống cột trong bảng DB
2. Giao diện (UI)
    - List để xem
    - Search, filter
    - Không cần code
    - Form để nhập
3. Quyền (Permission)
    - Ai được xem?
    - Ai được tạo?
    - Ai được xóa?
    -> Không phải viết middleware
4. Hành vi (Behavior)
    - Khi bấm Save → kiểm tra gì?
    - Khi Submit → làm gì?
```

# config/ – HẬU TRƯỜNG (SERVICE)
```bash
config/
├── redis_cache.conf
├── redis_queue.conf
├── pids/
├── ...

- Cấu hình service chạy nền
- Bench dùng để:
    + khởi động
    + quản lý
    + stop service
- Không sửa nếu chưa hiểu
```

# logs/ – HỘP ĐEN
```bash
logs/
└── bench.log

- Nơi debug
    + Frappe lỗi → vào đây
    + Bench không start → vào đây
    + 80% debug nhìn file này
```

# Procfile – KỊCH BẢN CHẠY
Nói cho Bench biết phải chạy những gì.
**Ex**
```bash
web
worker
scheduler

- Bench đọc file này khi start
```

# patches.txt – LỊCH SỬ CẬP NHẬT
```bash
- Ghi lại:
    + migration
    + patch DB
-Không sửa tay
``
```bash
- Frappe là một “hệ thống làm app quản lý” dựng sẵn gần như mọi thứ
- Nếu ví von:
    + Django / Spring = bộ khung + gạch + xi măng → bạn tự xây nhà
    + Microservice = cả khu đô thị → cần đội xây dựng chuyên nghiệp
    + Frappe = nhà lắp ghép cao cấp → chọn phòng, chọn cửa là ở được
- Frappe thực chất là 1 gói “ALL-IN-ONE”
    + Khi bạn dùng Frappe, bạn đã có sẵn:
        + Database
        + Backend (API)
        + Frontend (giao diện)
        + Login / User
- Phân quyền
    + CRUD
    + Form
    + Report
    + Workflow (duyệt, từ chối…)
    + Log, audit
- Bạn không phải hỏi: “Giờ làm giao diện kiểu gì, API ở đâu, auth sao đây?”
- Ví dụ đời thường (rất quan trọng): Bạn muốn làm app quản lý nhà đất
    + Không dùng Frappe:
        + Thiết kế DB
        + Viết model
        + Viết API
        + Viết form nhập
        + Viết trang list
        + Viết phân quyền
        + Viết report
- Dùng Frappe: Khai báo: Nhà đất có các cột: giá, diện tích, quận -> BẤM LƯU
    + Có luôn:
        + Bảng DB
        + Màn hình nhập
        + Màn hình xem
        + API
        + Quyền user
```

# Vì sao ERP dùng Frappe?
```bash
- ERP thực chất là:
    + Nhập dữ liệu
    + Sửa dữ liệu
    + Xem dữ liệu
    + Phân quyền
    + Duyệt
    + Báo cáo
-> Frappe sinh ra chỉ để làm mấy việc này cho nhanh và chuẩn
```