Thư viện py-vietnam-number là một lựa chọn tuyệt vời vì nó xử lý rất tốt các quy tắc lắt léo trong tiếng Việt như "mươi", "mười", "lăm", "lẻ/linh".

Dưới đây là hướng dẫn chi tiết để bạn cài đặt và test thử thư viện này.

1. Cài đặt thư viện
Vì đây là thư viện bên ngoài, bạn cần cài đặt nó thông qua công cụ pip. Hãy mở terminal (hoặc Command Prompt) và chạy lệnh sau:

Bash

pip install py-vietnam-number
2. Cách sử dụng cơ bản
Thư viện này cung cấp một class gọi là n2w (viết tắt của Number to Words).

Python

from vietnam_number import n2w

# Test thử số có 5 chữ số
print(n2w("12345")) 
# Kết quả: mười hai nghìn ba trăm bốn mươi lăm

# Test thử số lẻ (float)
print(n2w("105.5"))
# Kết quả: một trăm lẻ năm phẩy năm
3. Chương trình Test "xịn" cho yêu cầu của bạn
Kết hợp với vòng lặp while True và kiểm tra 5 chữ số mà chúng ta đã thảo luận ở trên, đây là bản demo hoàn chỉnh:

Python

from vietnam_number import n2w

print("--- CHƯƠNG TRÌNH ĐỌC SỐ VIỆT NAM ---")

while True:
    num_input = input("Nhập số nguyên có 5 chữ số (hoặc 'q' để thoát): ")
    
    if num_input.lower() == 'q':
        break
        
    # Kiểm tra điều kiện 5 chữ số và là số nguyên dương
    if num_input.isdigit() and len(num_input) == 5:
        try:
            doc_chu = n2w(num_input)
            print(f"👉 Cách đọc: {doc_chu.capitalize()}")
            print("-" * 30)
        except Exception as e:
            print(f"Có lỗi xảy ra: {e}")
    else:
        print("❌ Vui lòng nhập đúng 5 chữ số nguyên!")

print("Cảm ơn bạn đã sử dụng!")
4. Tại sao thư viện này "smooth" hơn code tự viết?
Thư viện này đã xử lý sẵn các trường hợp mà nếu tự viết bạn sẽ mất rất nhiều if-else:

Số 1: Đọc là "một" hay "mốt" (11 -> mười một, 21 -> hai mươi mốt).

Số 5: Đọc là "năm" hay "lăm" (15 -> mười lăm, 55 -> năm mươi lăm).

Số 0 ở giữa: Xử lý chữ "lẻ" hoặc "linh" (105 -> một trăm lẻ năm).

Hàng đơn vị: Xử lý "mươi" vs "mười" (10 -> mười, 20 -> hai mươi).

5. Một số tùy chọn khác (nếu cần)
Nếu bạn muốn dùng một thư viện khác cũng rất phổ biến và hỗ trợ nhiều ngôn ngữ (bao gồm tiếng Việt), bạn có thể thử num2words:

Bash

pip install num2words
Cách dùng:

Python

from num2words import num2words
print(num2words(12345, lang='vi'))
Lời khuyên: Nếu bạn chỉ làm việc với tiếng Việt, py-vietnam-number thường cho kết quả đọc nghe "xuôi tai" hơn theo phong cách địa phương.

Bạn đã cài đặt được thư viện chưa? Nếu gặp lỗi khi chạy lệnh pip, hãy báo mình để mình hỗ trợ sửa lỗi môi trường nhé!