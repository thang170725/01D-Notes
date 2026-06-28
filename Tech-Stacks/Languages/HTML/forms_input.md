- [input](#input)
- [button (Để tạo ra một nút bấm)](#button-để-tạo-ra-một-nút-bấm)
---
# input 
```bash
- Để lấy dữ liệu khi người dùng nhập vào.
```
**Syn**
```bash
<input 
    type=’file’ 
    accept='image/*' 
    value='' 
    name=''
    placeholder=''
>

- type : quy định chức năng của thẻ input đó.
    + text: tạo ra trường nhập văn bản.
    + password: trường nhập mật khẩu, các kí tự sẽ bị che đi bằng các ký tự *.
    + submit: tạo một nút bấm (để submit để nộp gửi lên form).
    + button: tạo một nút bấm.
    + checkbox: ô để tích.
    + Radio: ô để tích hình tròn.
    + Color: loại ô màu sác.
    + Date:
    + Time:
    + Search: tìm kiếm.
    + file: tạo ra trường thêm file.
    + range: tạo ra thanh kéo.
    + Week:
    + Number: kiểu số.
    + url: kiểu đường dẫn cho trang web.
    + email: kiểu email.
- accept : là thuộc tính của type=file, dùng để giới hạn loại file mà người dùng được chọn
    + image/* → nhóm MIME type của ảnh, tất cả định dạng ảnh
    + Cho phép: image/png, image/jpeg, image/jpg, image/webp, image/gif, image/svg+xml, … Không cho chọn: .exe, .pdf, .mp4, .zip
- value         : Để xác định giá trị mặc định cho ô đầu vào.   
- name          : Để xác tên cho ô đầu vào, dùng khi người dùng submit thông tin.
- placeholder   : Để đặt một văn bản mẫu cho ô đầu vào.
- required      : ô dữ liệu bắt buộc phải nhập trước khi submit file HTML lên sever.
- disabled      : Nếu giá trị là true thì đồng nghĩa người dùng không thể nhập hay thao tác với ô này.
- size          : Xác định độ rộng của ô đầu vào, giá trị là number + đơn vị
- max-length    : Xác định số kí tự tối đa mà người dùng được phép nhập vào ô
- min & max     : Xác định giá trị tối thiểu hay tối đa khi nhập ô đầu vào
- autocomplete  : Gợi ý các lựa chọn để người dùng nhập dữ liệu nhanh và dễ dàng hơn
- step          : Thường được sử dụng trong cá loại nhập số, dùng để xác định giá trị bước nhảy của ô
```
# button (Để tạo ra một nút bấm)