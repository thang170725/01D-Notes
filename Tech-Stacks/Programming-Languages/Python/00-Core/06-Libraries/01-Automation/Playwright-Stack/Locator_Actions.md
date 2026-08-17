- [page.locator()](#pagelocator)
  - [.nth()](#nth)
  - [.inner\_text()](#inner_text)
  - [.get\_attribute()](#get_attribute)
  - [.count()](#count)
---
# page.locator()
```bash
Tác dụng: Tạo ra một "vật trỏ" để tìm kiếm các phần tử trên trang (như nút bấm, ô nhập liệu, thẻ văn bản). Nó chưa lấy dữ liệu ngay mà chỉ xác định vị trí.
```
**Syn**
```bash
element = page.locator("tên_thẻ_hoặc_class_css")
```
**Ex**
```python
tieu_de = page.locator("h1") # Tìm tất cả các thẻ h1 trên trang
```
## .nth()
```bash
- Tác dụng: Chọn phần tử thứ n trong danh sách các phần tử tìm được (bắt đầu từ số 0).
```
**Syn** 
```bash
item = element.nth(0) (lấy phần tử đầu tiên).
```
**Ex**
```python
danh_sach = page.locator("li")
thu_nhat = danh_sach.nth(0) # Lấy dòng đầu tiên trong danh sách
```
## .inner_text()
```bash
Lấy nội dung chữ bên trong một phần tử.
```
**Syn**
```bash
chu = await element.inner_text()
```
**Ex**
```python
doan_van = page.locator("p") # Giả sử có thẻ <p>Chào bạn</p>
noidung = await doan_van.inner_text()
print(noidung) # Kết quả: Chào bạn
```
## .get_attribute()
```bash
- Lấy giá trị của một thuộc tính trong thẻ (thường dùng nhất là lấy link href hoặc link ảnh src).
```
**Syn** 
```bash
gia_tri = await element.get_attribute("tên_thuộc_tính")
```
**Ex**
```python
the_link = page.locator("a") # Lấy đường link của một thẻ <a>
url = await the_link.get_attribute("href")

print(url)
```
## .count()
```bash
- Đếm xem có bao nhiêu phần tử khớp với locator đã tìm.
```
**Syn** 
```bash
so_luong = await element.count()
```
**Ex**
```python
cac_nut = page.locator("button")
print(await cac_nut.count()) # In ra số lượng nút bấm có trên trang
```