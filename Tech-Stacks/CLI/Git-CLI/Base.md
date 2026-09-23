- [Directory Structure](#directory-structure)
- [Git introduction](#git-introduction)
  - [Repository (nơi Git lưu trữ toàn bộ lịch sử và trạng thái của một project)](#repository-nơi-git-lưu-trữ-toàn-bộ-lịch-sử-và-trạng-thái-của-một-project)
- [Installation](#installation)
---
# Directory Structure
```bash
GitHub/                # mình dùng thư mục này để xem kiến thức cơ bản của JS
├── IO_Config.md       # mình dùng file này để cấu hình, khởi tạo, đẩy lên và lấy về từ gitHub
├── Base.md            # mình dùng file này để xem kiến thức cơ bản và các tiện ích của JS
├── Process.md         # mình dùng file này để làm tất cả thao tác khác
├── File_Directory.md  # mình dùng file này để thao tác với file, thư mục
├── Branch/            # mình dùng file này để thao tác với nhánh
└── Practices.md       # mình dùng file này xem bài tập, các lệnh mẫu
```
# Git introduction 
## Repository (nơi Git lưu trữ toàn bộ lịch sử và trạng thái của một project)
**Ex**
```bash
Ví dụ bạn có project:
    json_service/
    ├── app/
    ├── tests/
    ├── requirements.txt
    └── README.md

Nếu chạy: git init -> Git sẽ tạo thêm:
    json_service/
    ├── app/
    ├── tests/
    ├── requirements.txt
    ├── README.md
    └── .git/ # Thư mục .git/ chính là Git repository ở local.
```
**Repository chứa những gì?**
```bash
Nó không chỉ chứa code, mà còn lưu:
    - Các commit trước đây
    - Lịch sử thay đổi của file
    - Branch (main, develop, feature/...)
    - Tag
    - Thông tin về remote repository
    - Trạng thái để Git biết file nào đã thay đổi
```
# Installation
**Linux**
```bash
1. sudo apt update
2. sudo apt install git
```