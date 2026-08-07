```text
Cần pip install django
```
**Kiểm tra**
```bash
django-admin --version
```

# Tạo project django
```bash
django-admin startproject myproject
```

# chạy server
```bash
cd house_price
python manage.py runserver
```

# Tạo app
python manage.py startapp core
```bash
core/
├── admin.py
├── apps.py
├── models.py
├── views.py
├── urls.py   (tự tạo)
└── migrations/
```