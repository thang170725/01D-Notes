- [Introduction](#introduction)
- [Installation](#installation)
---
# Introduction
```bash
- PyInstaller là một công cụ Python dùng để đóng gói chương trình Python thành file thực thi độc lập (.exe trên Windows, hoặc binary trên Linux/macOS).
- PyInstaller không hỗ trợ cross-compile chính thức.
    Nghĩa là:
        Build trên Windows → ra .exe Windows
        Build trên Linux → ra binary Linux
        Build trên macOS → ra binary macOS
- Ví dụ:
    # Linux
    pyinstaller --onefile app.py

    sẽ tạo:
        dist/app
    chứ không phải:
        dist/app.exe

    Muốn có .exe Windows, bạn thường phải:
        Build trên Windows.
        Hoặc dùng CI/CD như GitHub Actions chạy trên Windows.
        Hoặc dùng Wine (khá nhiều trường hợp phát sinh lỗi).
```
**Ex**
```bash
- Ví dụ:
    pip install pyinstaller

    Sau đó:
        pyinstaller app.py

        PyInstaller sẽ:
            - Phân tích các thư viện mà app.py import.
            - Gom Python interpreter + thư viện + code của bạn.
            - Tạo file thực thi để chạy trên máy không cần cài Python.

    Ví dụ tạo một file .exe duy nhất:
        pyinstaller --onefile app.py

    Sau khi chạy sẽ có:
        project/
        ├── build/
        ├── dist/
        │   └── app.exe
        ├── app.spec
        └── app.py

    - File thực thi nằm trong:
        dist/app.exe
```
# Installation
```bash
1. pip install pyinstaller
```
