# Installation
```bash
1. sudo apt update
2. sudo apt install wget gpg
3. wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
4. sudo install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/
5. sudo sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] \
https://packages.microsoft.com/repos/code stable main" > /etc/apt/sources.list.d/vscode.list'
6. sudo apt update
7. sudo apt install code# shortcut vscode linux
```
# Shortcut
```bash
1. Alt + ↑: Di chuyển cả dòng lệnh tại con trỏ lên phía trên.
2. Alt + E: mở tab edit vs code.
3. Alt + F: mở tab file trong vs code.
4. Alt + V: Mở tab view trong vs code.

1. Shift + alt + ↑: Chỉ định viết mấy dòng một lần
2. Shift + ←: đưa con trỏ sang trái đồng thời xóa bôi đen

1.  Ctrl + l            : Bôi đen cả dòng tại con trỏ chuột.
2.  Ctrl + d            : Thêm vùng chọn vào kết quả find phù hợp.
3.  Ctrl + /            : Comment 1 dòng tại vị trí con trỏ chuột.
4.  Ctrl + shift + k    : Xóa một dòng tại vị trí con trỏ chuột
5.  Ctrl + ]            : Cả dòng lùi vào một kích thước khoản trắng =  1 tab
6.  Ctrl + A            : Chọn toàn bộ đoạn chữ.
7.  Ctrl + C            : Copy chữ.
8.  Ctrl + F            : tìm chữ.
9.  Ctrl + H            : Tìm và thay thế chữ.
10. Ctrl + N            : Tạo một tài liệu mới.
11. Ctrl + O            : Mở một file.
12. Ctrl + P            : Đi đến một file khác.
13. Ctrl + S            : Lưu file.
14. Ctrl + V            : paste file.
15. Ctrl + X            : Cắt một đoạn chữ (cắt theo từng dòng).
16. Ctrl + Y            : Redo text.
17. Ctrl + Z            : Undo text.
18. Ctrl + Home         : Đưa con trỏ lên đầu của file hiện tại.
19. Ctrl + End          : Đưa con trỏ xuống cuối của file hiện tại. 
20. Ctrl + →            : Con trỏ sang đúng bằng một chữ.
21. Ctrl + ←            : Đưa con trỏ sang trái đúng bằng một chữ.
22. Ctrl + shift + I    : Sắp xếp các dòng lệnh cho đẹp mắt, dễ nhìn.
```
# Preferences: Open Workspace Settings (JSON)
```bash
1. Ctrl + Shift + P
2. gõ: Preferences: Open Workspace Settings (JSON)
```