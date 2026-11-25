- [System Introduction (là thư viện chứa các chức năng cơ bản có sẵn trong C sharp giúp lập trình viên không phải tự viết lại từ đầu)](#system-introduction-là-thư-viện-chứa-các-chức-năng-cơ-bản-có-sẵn-trong-c-sharp-giúp-lập-trình-viên-không-phải-tự-viết-lại-từ-đầu)
- [Xml (là namespace dùng để đọc ghi tạo và xử lý dữ liệu XML)](#xml-là-namespace-dùng-để-đọc-ghi-tạo-và-xử-lý-dữ-liệu-xml)
  - [XmlDocument (đại diện cho toàn bộ tài liệu XML)](#xmldocument-đại-diện-cho-toàn-bộ-tài-liệu-xml)
    - [.Load()	(Đọc XML từ file)](#loadđọc-xml-từ-file)
      - [Save()	(Lưu XML xuống file)](#savelưu-xml-xuống-file)
      - [CreateElement() (Tạo phần tử XML)](#createelement-tạo-phần-tử-xml)
        - [InnerText (Lấy hoặc gán nội dung văn bản)](#innertext-lấy-hoặc-gán-nội-dung-văn-bản)
        - [InnerXml (Lấy hoặc gán nội dung XML bên trong)](#innerxml-lấy-hoặc-gán-nội-dung-xml-bên-trong)
        - [Attributes (Truy cập các thuộc tính của phần tử)](#attributes-truy-cập-các-thuộc-tính-của-phần-tử)
        - [Name (Lấy tên phần tử)](#name-lấy-tên-phần-tử)
      - [CreateAttribute() (Tạo thuộc tính XML)](#createattribute-tạo-thuộc-tính-xml)
      - [DocumentElement() (Lấy phần tử gốc)](#documentelement-lấy-phần-tử-gốc)
      - [XmlElement (Đại diện cho một phần tử XML)](#xmlelement-đại-diện-cho-một-phần-tử-xml)
      - [XmlAttribute (Tạo và quản lý thuộc tính của phần tử XML)](#xmlattribute-tạo-và-quản-lý-thuộc-tính-của-phần-tử-xml)
  - [XmlNode (Đại diện cho một nút trong tài liệu XML)](#xmlnode-đại-diện-cho-một-nút-trong-tài-liệu-xml)
  - [XmlNodeList (Đại diện cho danh sách nút trong tài liệu XML)](#xmlnodelist-đại-diện-cho-danh-sách-nút-trong-tài-liệu-xml)
      - [AppendChild() (Thêm nút con)](#appendchild-thêm-nút-con)
      - [RemoveChild() (Xóa nút con)](#removechild-xóa-nút-con)
      - [ReplaceChild() (Thay nút cũ bằng nút mới)](#replacechild-thay-nút-cũ-bằng-nút-mới)
      - [SelectSingleNode() (Tìm một nút theo XPath)](#selectsinglenode-tìm-một-nút-theo-xpath)
      - [SelectNodes() (Tìm nhiều nút theo XPath)](#selectnodes-tìm-nhiều-nút-theo-xpath)
---
# System Introduction (là thư viện chứa các chức năng cơ bản có sẵn trong C sharp giúp lập trình viên không phải tự viết lại từ đầu)
**Ex** 
```bash
nhập dữ liệu, in ra màn hình, xử lý chuỗi, tính toán, lấy ngày giờ và xử lý lỗi.
```
# Xml (là namespace dùng để đọc ghi tạo và xử lý dữ liệu XML)
**Ex**
```bash
- Đọc dữ liệu từ file XML.
- Tạo và chỉnh sửa file XML.
- Tìm kiếm dữ liệu trong XML.
- Phân tích cấu trúc XML.
```
## XmlDocument (đại diện cho toàn bộ tài liệu XML)
**Syn**
```bash
XmlDocument doc = new XmlDocument();
```
### .Load()	(Đọc XML từ file)
**Ex**
```c#
XmlDocument doc = new XmlDocument();
string duongDanFile = @"D:\HanoiUniversityOfIndustryCourse\HK7\tich_hop_htpm\Tx2\XMLFile1.xml";

private void HienThi(object sender, EventArgs e)
{
    // 1. load file xml
    doc.Load(duongDanFile);
}
```
#### Save()	(Lưu XML xuống file)
#### CreateElement() (Tạo phần tử XML)
**Ex**
```c#
XmlElement ho = doc.CreateElement("ho");

ho.InnerText = "Nguyen Van";

MessageBox.Show(ho.InnerText); // Nguyen Van
```
##### InnerText (Lấy hoặc gán nội dung văn bản)
**Ex**
```csharp
XmlElement ho = doc.CreateElement("ho");

ho.InnerText = "Nguyen Van";

MessageBox.Show(ho.InnerText); // Nguyen Van
```
##### InnerXml (Lấy hoặc gán nội dung XML bên trong)
##### Attributes (Truy cập các thuộc tính của phần tử)
##### Name (Lấy tên phần tử)
#### CreateAttribute() (Tạo thuộc tính XML)
#### DocumentElement() (Lấy phần tử gốc)
**Ex**
```xml
<ds>
    <nhanvien manv="NV01"/>
</ds>
```
```csharp
XmlElement theGoc = doc.DocumentElement; // theGoc đại diện cho thẻ <ds>.
```
#### XmlElement (Đại diện cho một phần tử XML)
**Syn**
```csharp
XmlElement nhanVien = doc.CreateElement("nhanvien"); // Kết quả tạo ra phần tử: <nhanvien />
```
#### XmlAttribute (Tạo và quản lý thuộc tính của phần tử XML)
**Ex**
```xml
<nhanvien manv="NV01"/>
```
```csharp
XmlAttribute maNV = doc.CreateAttribute("manv"); // Tạo thuộc tính tên manv.

maNV.InnerText = "NV01"; // Gán giá trị thuộc tính.
```
## XmlNode (Đại diện cho một nút trong tài liệu XML)
## XmlNodeList (Đại diện cho danh sách nút trong tài liệu XML)
#### AppendChild() (Thêm nút con)
#### RemoveChild() (Xóa nút con)
#### ReplaceChild() (Thay nút cũ bằng nút mới)
#### SelectSingleNode() (Tìm một nút theo XPath)
**Syn**
XmlNode node = doc.SelectSingleNode("đường_dẫn_XPath");
#### SelectNodes() (Tìm nhiều nút theo XPath)
**Syn**
```bash
XmlNodeList danhSach = doc.SelectNodes("đường_dẫn_XPath");
```


Ví dụ có file XML:
<ds>
    <nhanvien manv="NV01">
        <hoten>
            <ho>Nguyen</ho>
            <ten>An</ten>
        </hoten>
        <diachi>Ha Noi</diachi>
    </nhanvien>

    <nhanvien manv="NV02">
        <hoten>
            <ho>Tran</ho>
            <ten>Binh</ten>
        </hoten>
        <diachi>Da Nang</diachi>
    </nhanvien>
</ds>


Muốn tìm nhân viên NV01:
XmlNode nv = doc.SelectSingleNode("/ds/nhanvien");


Kết quả: Lấy nhân viên đầu tiên trong danh sách.

Muốn lấy nhân viên có mã NV02:
XmlNode nv = doc.SelectSingleNode(
    "/ds/nhanvien[@manv='NV02']"
);


Kết quả: Lấy nút nhân viên NV02.

Giải thích XPath:
Thành phần	Ý nghĩa
/	Bắt đầu từ nút gốc
ds	Thẻ gốc
nhanvien	Thẻ nhân viên
@manv	Thuộc tính manv
[@manv='NV02']	Điều kiện mã nhân viên bằng NV02

Nếu không tìm thấy, SelectSingleNode() trả về null.

Vì vậy thường phải kiểm tra:
if (nv != null)
{
    MessageBox.Show("Tìm thấy nhân viên!");
}
else
{
    MessageBox.Show("Không tìm thấy!");
}
**Ex2: Tìm và lấy tất cả các nút thỏa mãn điều kiện**
```c#
XmlNodeList danhSach = doc.SelectNodes("/ds/nhanvien");

foreach (XmlNode nv in danhSach)
{
    MessageBox.Show(nv.Attributes["manv"].Value);
}

// Kết quả:
// NV01
// NV02
```

4. Lấy dữ liệu bên trong thẻ XML
Ví dụ:
<nhanvien manv="NV01">
    <hoten>
        <ho>Nguyen</ho>
        <ten>An</ten>
    </hoten>
    <diachi>Ha Noi</diachi>
</nhanvien>


Cách 1: Dùng SelectSingleNode()
XmlNode nv = doc.SelectSingleNode(
    "/ds/nhanvien[@manv='NV01']"
);

if (nv != null)
{
    string diaChi = nv.SelectSingleNode("diachi").InnerText;

    MessageBox.Show(diaChi);
}


Kết quả:
Ha Noi


Ở đây:
- nv: Nút nhân viên.
- SelectSingleNode("diachi"): Tìm thẻ địa chỉ bên trong nhân viên.
- InnerText: Lấy nội dung của thẻ.
Cách 2: Dùng Attributes
Lấy mã nhân viên:
string ma = nv.Attributes["manv"].Value;


Kết quả:
NV01


So sánh hai cách:
// Lấy nội dung thẻ
string diaChi = nv.SelectSingleNode("diachi").InnerText;

// Lấy giá trị thuộc tính
string ma = nv.Attributes["manv"].Value;


Đây là hai cách rất hay gặp trong đề thi.

5. Kết hợp XML với DataGridView
Đây là ví dụ thực tế để đưa dữ liệu XML lên bảng.
private void HienThi()
{
    doc.Load(duongDanFile);

    table.Rows.Clear();

    XmlNodeList danhSach = doc.SelectNodes("/ds/nhanvien");

    foreach (XmlNode nv in danhSach)
    {
        string ma = nv.Attributes["manv"].Value;

        string ho = nv.SelectSingleNode("hoten/ho").InnerText;

        string ten = nv.SelectSingleNode("hoten/ten").InnerText;

        string diaChi = nv.SelectSingleNode("diachi").InnerText;

        table.Rows.Add(ma, ho, ten, diaChi);
    }
}


Giải thích luồng chạy:
1. Đọc file XML bằng Load().
2. Xóa dữ liệu cũ trên DataGridView bằng Rows.Clear().
3. Lấy danh sách nhân viên bằng SelectNodes().
4. Dùng foreach duyệt từng nhân viên.
5. Lấy mã, họ, tên và địa chỉ.
6. Dùng Rows.Add() đưa dữ liệu lên bảng.
Kết quả hiển thị:
Danh sách nhân viên
Mã NV	Họ	Tên	Địa chỉ
NV01	Nguyen	An	Ha Noi
NV02	Tran	Binh	Da Nang


Lưu ý: Ví dụ trên giả sử XML có đầy đủ các thẻ và thuộc tính cần thiết. Nếu dữ liệu có thể thiếu, cần kiểm tra null trước khi gọi .InnerText hoặc .Value.