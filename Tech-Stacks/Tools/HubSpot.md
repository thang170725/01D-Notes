+ [<<Back](Base.md)
- [HubSpot và HubSpot API là hai thứ liên quan chặt với nhau:](#hubspot-và-hubspot-api-là-hai-thứ-liên-quan-chặt-với-nhau)
---
# HubSpot (Customer Relationship Management dùng để doanh nghiệp quản lý khách hàng và hoạt động bán hàng/marketing)
**Ex: Ví dụ một công ty có 100.000 khách hàng**
```bash
Khách hàng
   ├── Thông tin liên hệ
   ├── Công ty
   ├── Email
   ├── Cuộc gọi
   ├── Lịch sử mua hàng
   ├── Deal
   └── Support ticket

HubSpot lưu và quản lý những dữ liệu này.

Các phần phổ biến của HubSpot:
  - CRM → quản lý customer/contact/company
  - Marketing → email marketing, campaign
  - Sales → quản lý lead, deal, pipeline
  - Service → support/ticket
  - Automation → tự động hóa workflow
  - Analytics → báo cáo, thống kê
```
# HubSpot API (là cách để chương trình của bạn giao tiếp với HubSpot)
**Ex1: Ví dụ bình thường bạn mở HubSpot trên trình duyệt**
```bash
Bạn -> HubSpot UI -> Database HubSpot

Nhưng nếu bạn là developer và muốn lấy dữ liệu bằng Python:
  Python program -> HubSpot API -> HubSpot -> Database
```
**Ex2: Ví dụ bạn muốn lấy danh sách contact.**
```python
import requests

url = "https://api.hubapi.com/crm/v3/objects/contacts"
headers = {"Authorization": "Bearer YOUR_ACCESS_TOKEN"}

response = requests.get(url, headers=headers)

data = response.json()

print(data)
# {
#   "results": [
#     {
#       "id": "123",
#       "properties": {
#         "email": "alice@example.com",
#         "firstname": "Alice",
#         "lastname": "Nguyen"
#       }
#     }
#   ]
# }
```