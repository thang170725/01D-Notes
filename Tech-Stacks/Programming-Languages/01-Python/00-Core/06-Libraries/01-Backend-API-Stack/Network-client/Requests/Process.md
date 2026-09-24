- [Bound I/O](#bound-io)
  - [.get()](#get)
  - [.post()](#post)
- [Display (Nhóm cung cấp thông tin)](#display-nhóm-cung-cấp-thông-tin)
  - [response.status\_code	Mã trạng thái (200, 404…)](#responsestatus_codemã-trạng-thái-200-404)
  - [response.text	Nội dung dạng string](#responsetextnội-dung-dạng-string)
  - [response.json()	Parse JSON → dict](#responsejsonparse-json--dict)
  - [response.headers	Header trả về](#responseheadersheader-trả-về)
- [Update (Nhóm cấp nhật)](#update-nhóm-cấp-nhật)
  - [requests.put()](#requestsput)
- [Delete (Nhóm xóa)](#delete-nhóm-xóa)
  - [requests.delete()](#requestsdelete)
- [requests.request() (tổng quát)](#requestsrequest-tổng-quát)
---
# Bound I/O
## .get()
```bash
Dùng để gửi request → server
```
**Syn**
```bash
requests.get(url, params=None, headers=None)

- Input:
    + url: địa chỉ API
    + params: query string (dict)
    + headers: header (token, user-agent…)
- Output:
    + Response object
```
**Ex**
```bash
import requests

response = requests.get("https://example.com")
```
## .post()
```bash
Dùng để gửi dữ liệu lên server
```
**Syn**
```bash
requests.post(url, data=None, json=None)

- Input:
    + data: gửi form (key=value)
    + json: gửi JSON (tự encode)
- Output:
    + Response object
```
**Ex**
```python
import requests

data = {"username": "thang", "password": "123"}
res = requests.post("https://httpbin.org/post", data=data)

print(res.json())
```
# Display (Nhóm cung cấp thông tin)
## response.status_code	Mã trạng thái (200, 404…)
## response.text	Nội dung dạng string
## response.json()	Parse JSON → dict
## response.headers	Header trả về
# Update (Nhóm cấp nhật)
## requests.put()
```bash 
Dùng để cập nhật dữ liệu
```
**Syn**
```bash
requests.put(url, data=None)
```
**Ex**
```python
res = requests.put("https://httpbin.org/put", data={"name": "new"})
print(res.json())
```
# Delete (Nhóm xóa)
## requests.delete()

👉 Dùng để xóa dữ liệu

Cú pháp:
requests.delete(url)
Ví dụ:
res = requests.delete("https://httpbin.org/delete")
print(res.status_code)
# requests.request() (tổng quát)

👉 Hàm “gốc” của tất cả các hàm trên

Cú pháp:
requests.request(method, url, **kwargs)
Ví dụ:
res = requests.request("GET", "https://httpbin.org/get")
print(res.status_code)
🔑 4. Một số tham số quan trọng
✔ headers
headers = {"Authorization": "Bearer TOKEN"}
requests.get(url, headers=headers)
✔ params (query string)
requests.get(url, params={"page": 1})

👉 URL thành:

? page=1
✔ timeout
requests.get(url, timeout=5)

👉 Tránh treo chương trình

✔ cookies
requests.get(url, cookies={"session_id": "abc"})
⚠️ 5. Xử lý lỗi
res = requests.get("https://api.github.com")

if res.status_code == 200:
    print("OK")
else:
    print("Error")

Hoặc:

res.raise_for_status()