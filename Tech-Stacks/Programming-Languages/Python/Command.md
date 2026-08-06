- [Installation](#installation)
- [python --veraion (Kiểm tra xem python đã được cài vào máy hay chưa)](#python---veraion-kiểm-tra-xem-python-đã-được-cài-vào-máy-hay-chưa)
  - [deactivate (Thoát khỏi môi trường ảo hiện tại)](#deactivate-thoát-khỏi-môi-trường-ảo-hiện-tại)
  - [which python (Linux/MacOS) | Get-Command python hoặc gcm python (Windows) (Xem đường dẫn môi trường run python trỏ đến đâu)](#which-python-linuxmacos--get-command-python-hoặc-gcm-python-windows-xem-đường-dẫn-môi-trường-run-python-trỏ-đến-đâu)
  - [where.exe python (Windows)](#whereexe-python-windows)
---
[Back](../Base.md)
# Installation
**Linux Installation**
**Ex: Cài đặt Python3.10**
```bash
1. sudo add-apt-repository ppa:deadsnakes/ppa
2. sudo apt update
3. sudo apt install python3.10
```
# python --veraion (Kiểm tra xem python đã được cài vào máy hay chưa)
```bash
1. python --version | python3.10 --version
```
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
## deactivate (Thoát khỏi môi trường ảo hiện tại)
## which python (Linux/MacOS) | Get-Command python hoặc gcm python (Windows) (Xem đường dẫn môi trường run python trỏ đến đâu)
## where.exe python (Windows)