Sys
    • Tương tác trực tiếp với trình thông dịch Python. Dùng để lấy tham số dòng lệnh (sys.argv), quản lý đường dẫn hệ thống (sys.path), hoặc thoát chương trình.
    • Thư viện không cần tải, cần import sys
.exit()
Dùng để dừng chương trình đột ngột.
Cú pháp:
import sys
for i in range(1, 10, 1):
    print(i)
    if(i == 5):
        sys.exit() # dừng chương trình'
print("in tao ra")
1
2
3
4
5
# tất cả phần dưới không chạy
