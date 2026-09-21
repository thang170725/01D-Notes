- [OS Introduction (Dùng để tổng hợp kiến thức liên quan đến hệ điều hành)](#os-introduction-dùng-để-tổng-hợp-kiến-thức-liên-quan-đến-hệ-điều-hành)
- [Linux](#linux)
  - [Apt (là trình quản lý package truyền thống của Ubuntu/Debian)](#apt-là-trình-quản-lý-package-truyền-thống-của-ubuntudebian)
  - [Snap (hệ thống package của Canonical)](#snap-hệ-thống-package-của-canonical)
  - [Ask](#ask)
    - [Snap khác gì so với apt?](#snap-khác-gì-so-với-apt)
    - [theo bạn mô tả thì tôi thấy snap có vẻ tốt hơn nhưng sao nhiều người lại không thích dùng](#theo-bạn-mô-tả-thì-tôi-thấy-snap-có-vẻ-tốt-hơn-nhưng-sao-nhiều-người-lại-không-thích-dùng)
---
# OS Introduction (Dùng để tổng hợp kiến thức liên quan đến hệ điều hành)
# Linux
## Apt (là trình quản lý package truyền thống của Ubuntu/Debian)
**Ex**
```bash
sudo apt install curl

APT thường cài:
    - chương trình
    - các thư viện mà chương trình cần
    - file cấu hình
    - dependency từ hệ thống
    - Các package thường lấy từ repository của Ubuntu/Debian.
```
## Snap (hệ thống package của Canonical)
**Ex**
```bash
sudo snap install aws-cli --classic

# Snap thường đóng gói ứng dụng + phần lớn dependency cần thiết thành một package.
# Điểm đặc trưng là Snap có cơ chế sandbox và tự động cập nhật.
```
## Ask
### Snap khác gì so với apt?
```bash
Nếu bạn đang nói về cài phần mềm trên Ubuntu bằng snap so với apt, thì khác nhau chủ yếu ở cách đóng gói, cập nhật và quản lý dependency.

So sánh nhanh:
    	                apt	                                    snap
    Kiểu package	    .deb	                                .snap
    Nguồn chính	        Ubuntu/Debian                           repositories	Snap Store
    Dependency	        Dùng nhiều thư viện của hệ thống	    Thường đóng gói dependency riêng
    Dung lượng	        Thường nhỏ hơn	                        Thường lớn hơn
    Cập nhật	        Bạn thường chạy apt upgrade	            Tự động cập nhật
    Cách ly ứng dụng	Ít hơn	                                Có sandbox
    Tốc độ mở app	    Thường nhanh	                        Một số app có thể chậm hơn lúc khởi động
    Phiên bản	        Có thể khá ổn định nhưng đôi khi cũ	    Thường dễ có phiên bản mới
    Gỡ	                sudo apt remove xxx	                    sudo snap remove xxx
```
### theo bạn mô tả thì tôi thấy snap có vẻ tốt hơn nhưng sao nhiều người lại không thích dùng
```bash
Đúng, nếu chỉ nhìn vào các ưu điểm thì Snap có vẻ rất tiện. Nhưng lý do nhiều người Linux không thích Snap là vì họ đánh đổi một số thứ mà người dùng Linux khá coi trọng: hiệu năng, tính minh bạch, quyền kiểm soát và sự tích hợp với hệ thống.

Có thể hiểu qua ví dụ này:

1. Snap thường nặng hơn

Snap thường đóng gói nhiều dependency bên trong package.

Ví dụ cùng một ứng dụng:

APT
┌──────────────────────┐
│ App                  │
│ dùng thư viện Ubuntu │
└──────────────────────┘

SNAP
┌──────────────────────┐
│ App                  │
│ dependency           │
│ runtime              │
│ libraries            │
└──────────────────────┘

Vì vậy Snap có thể:

chiếm nhiều dung lượng hơn
có nhiều file mount
đôi khi khởi động ứng dụng chậm hơn

Với một CLI nhỏ thì vấn đề này có thể không đáng kể. Nhưng với desktop app thì người dùng dễ nhận thấy hơn.

2. Snap tự động cập nhật

Đây vừa là ưu điểm vừa là nhược điểm.

Snap có cơ chế refresh tự động.

Ví dụ bạn đang dùng:

my-app 1.5

Sau đó Snap tự cập nhật:

my-app 1.6

Với người dùng bình thường:

"Tốt, khỏi phải tự cập nhật."

Nhưng với người làm server/dev:

"Khoan, tôi muốn tự quyết định lúc nào update."

Đặc biệt nếu version mới làm thay đổi behavior hoặc gây incompatibility thì automatic update có thể gây khó chịu.

APT cũng có cập nhật tự động trong một số cấu hình Ubuntu, nhưng cách quản lý package của APT thường cho người dùng nhiều quyền kiểm soát trực tiếp hơn.

3. Snap phụ thuộc vào Snap Store

Đây là một điểm khiến một bộ phận người dùng Linux không thích.

APT sử dụng hệ thống repository/package của Debian/Ubuntu:

Ubuntu repositories
        ↓
      APT
        ↓
     .deb

Snap:

Snap Store
     ↓
    snap
     ↓
   ứng dụng

Snap Store do Canonical vận hành.

Một số người trong cộng đồng Linux thích mô hình:

"Tôi muốn package nằm trong repository của distro và được quản lý bằng công cụ native của distro."

Họ không thích việc thêm một lớp ecosystem khác.

4. Snap dùng mount/loop filesystem

Đây là một đặc điểm kỹ thuật khá dễ nhận thấy.

Nếu chạy:

snap list

bạn sẽ thấy các Snap đã cài.

Và:

df -h

có thể thấy nhiều filesystem dạng:

/dev/loop...

Đó là vì Snap package thường được đóng gói dưới dạng filesystem image và được mount.

Người mới có thể thấy:

Tại sao tôi cài 5 app mà có cả đống /dev/loop?

😄

Không phải lỗi, đó là cách Snap hoạt động.

5. Sandbox đôi khi gây phiền

Sandbox là một ưu điểm về bảo mật.

Nhưng đôi khi nó khiến ứng dụng không truy cập được thứ mà bạn nghĩ rằng nó phải truy cập được.

Ví dụ:

Application
     │
     ├── muốn đọc file
     │
     └── Sandbox
             ↓
        "Không được phép"

Sau đó phải kiểm tra các interface/permission của Snap.

Trong khi với một package .deb thông thường:

sudo apt install myapp

ứng dụng thường tích hợp trực tiếp với filesystem của hệ thống.

6. Một số người không thích Snap vì trải nghiệm desktop

Đặc biệt với các ứng dụng GUI, người dùng có thể gặp những vấn đề như:

startup chậm hơn
theme không khớp hoàn toàn
permission hơi khó hiểu
tích hợp filesystem không giống package native
một số extension/plugin hoạt động khác

Không phải Snap app nào cũng gặp những vấn đề này.

Nhưng có một điều quan trọng

"Nhiều người không thích Snap" ≠ "Snap là công nghệ tệ".

Snap giải quyết một vấn đề rất thực tế:

Làm sao đóng gói một ứng dụng để nó chạy tương đối độc lập trên nhiều phiên bản Linux?

Đây cũng chính là lý do tồn tại của những công nghệ như:

.deb       → package truyền thống
Snap       → application package
Flatpak    → application package
AppImage   → portable application
Docker     → container

Mỗi cái có mục tiêu hơi khác nhau.

Với trường hợp của bạn

Bạn đang học Ubuntu + AWS CLI + LocalStack, nên mình sẽ nhìn thế này:

AWS CLI
   │
   ├── apt  → nếu repository có version phù hợp
   │ai
   └── snap → dễ cài version mới

Việc bạn dùng:

sudo snap install aws-cli --classic

hoàn toàn ổn.

Đối với một CLI như AWS CLI, bạn không cần quá lo chuyện Snap nặng hay startup GUI chậm. Bạn chỉ cần nhớ cách kiểm tra:

snap list

và:

aws --version

Nếu sau này bạn học sâu hơn về Linux administration/server, lúc đó mình khuyên bạn nên hiểu cả APT, Snap, Flatpak và Docker, vì chúng giải quyết những bài toán khác nhau.
```