# Mô hình quản lý công việc

## Flow chart
**Phân tích dựa vào ví dụ**
```text
Lấy ví dụ về Công ty cha (eKGis) có nhiều công ty con MBW, Fast, v.v
```
```text
[workspace]     : Mỗi workspace là một công ty con MBW, Fast trong hệ thống của công ty cha (eKGis) - Plane.
     ↓
 [project]      : Trong mỗi công ty lại làm nhiều dự án cùng lúc (Bất động sản, Bán hàng, v.v)
     ↓  
  [epics]       : Mỗi dự án cần chia ra các chủ để lớn (Ví dụ: Bán hàng: Quản lý người dùng, nhóm chức năng mua sắm, v.v)
     ↓ 
[Work items]    : Mỗi một epic lại chia thành các đầu việc nhỏ hơn và cụ thể hơn (Nhóm chức năng mua sắm: Mua, thanh toán, xem sản 
     ↓            phầm, v.v)
 [Modules]      : Là khối nhỏ nhất (Thanh toán cần có form gì, nút gì, v.v)

- trang workspace chỉ quản lý mới có quyền truy cập có thể (thao tác được bất kỳ cái gì trong giới hạn hệ thống).
- member (tức thành viên tham gia dự án nào đó) chỉ có quyền thao tác trên tran project đó.
```

## Work items - công việc cụ thể
```text
Với các work items cần tuân thủ Cycles (Chu kỳ giống sprint).
```
**Cycles**
```text
- Là khoảng thời gian để  hoàn thành 1 work item (Ví dụ: 5 ngày, 1 tuần).
- Cycles có các trạng thái (đang hoạt động - work item sắp tới - hoàn thành)
```
**Timeline dependencies**
```text
- Là liện hệ giữa các task với nhau.
```