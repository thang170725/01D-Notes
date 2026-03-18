- [Blur](#blur)
  - [Gussian Blur](#gussian-blur)
# Blur
## Gussian Blur
**Cách hoạt động**
```bash
Giả sử chúng ta muốn tính giá trị của pixel tại vị trí (1,1), giá trị 60 trong ví dụ. Chúng ta sẽ đặt môt kernel 3x3 lên ma trận ảnh sao cho trung tâm của kernel đó trùng với pixel(1,1).
Các pixel xung quanh pixel (1,1) trong ma trận ảnh gốc sẽ là:
```
```bash
Bây giờ, chúng ta sẽ thực hiện phép tích chập:
Giá trị pixel mới tại (1,1) sẽ là: 
= (10×0.0625)+(20×0.125)+(30×0.0625)+ (50×0.125)+(60×0.25)+(70×0.125)+ (90×0.0625)+(100×0.125)+(110×0.0625)
= 0.625+2.5+1.875+ 6.25+15+8.75+ 5.625+12.5+6.875
= 65
Vậy, giá trị pixel mới tại vị trí (1,1) trong ma trận kết quả sẽ là 65.
```