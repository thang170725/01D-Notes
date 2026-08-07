- [Linux](#linux)
- [Installation](#installation)
  - [deactivate (Thoát khỏi môi trường ảo hiện tại)](#deactivate-thoát-khỏi-môi-trường-ảo-hiện-tại)
  - [which python (Linux/MacOS) |](#which-python-linuxmacos-)
  - [where.exe python (Windows)](#whereexe-python-windows)
- [Windows](#windows)
  - [Get-Command python | gcm python (Xem đường dẫn môi trường run python trỏ đến đâu)](#get-command-python--gcm-python-xem-đường-dẫn-môi-trường-run-python-trỏ-đến-đâu)
- [Python](#python)
- [python --veraion (Kiểm tra xem python đã được cài vào máy hay chưa)](#python---veraion-kiểm-tra-xem-python-đã-được-cài-vào-máy-hay-chưa)
- [site](#site)
- [Tạo môi trường ảo \& activate](#tạo-môi-trường-ảo--activate)
---
[<<Back](Base.md)
# Linux
# Installation
**Linux Installation**
**Ex: Cài đặt Python3.10**
```bash
1. sudo add-apt-repository ppa:deadsnakes/ppa
2. sudo apt update
3. sudo apt install python3.10
```
## deactivate (Thoát khỏi môi trường ảo hiện tại)
## which python (Linux/MacOS) | 
## where.exe python (Windows)
# Windows
## Get-Command python | gcm python (Xem đường dẫn môi trường run python trỏ đến đâu)
# Python
# python --veraion (Kiểm tra xem python đã được cài vào máy hay chưa)
```bash
1. python --version | python3.10 --version
```
# site
```bash
2. python –m site | python –m site --user-site  : Hiển thị thông tin cài đặt python và các thư mục liên quan.
3. pip list                                     : kiểm tra tất cả các thư viện đã cài đặt.
4. pip show numpy                               : kiểm tra thư viện numpy đã cài vào máy chưa.
```
# Tạo môi trường ảo & activate
**Tạo và kích hoạt**
```bash
1. New terminal
2. python3 -m venv D:\python_env
3. D:\python_env\Scripts\activate (Windows) | source env/bin/activate (Linux)
```