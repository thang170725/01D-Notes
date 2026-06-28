# DBSCAN (Density-Based Spatial Clustering of Applications with Noise) 
```bash
là một thuật toán phân cụm (clustering) dựa trên mật độ điểm dữ liệu.

Nói đơn giản:
    - Nếu nhiều điểm nằm gần nhau → chúng thuộc cùng một nhóm.
    - Nếu một điểm đứng một mình, không gần nhóm nào → nó là nhiễu (noise).
```
**Ex**
```bash
Hãy tưởng tượng bạn nhìn từ trên cao xuống một bãi biển.

Có rất nhiều người đứng thành từng nhóm.

      ● ● ●
    ● ● ● ●

                       ● ●
                     ● ● ●

      x

                                 ● ● ●
                               ● ● ●

Các cụm người đứng sát nhau → 3 cluster.
Người đứng một mình (x) → Noise.

DBSCAN sẽ tìm ra:
    - Cluster 1
    - Cluster 2
    - Cluster 3
    - Noise
```
**DBSCAN hoạt động như thế nào?**
```bash
Thuật toán chỉ cần 2 tham số.

1. eps (ε)
    Là bán kính tìm hàng xóm.

    Ví dụ
          ●
        eps = 2m
    => Nếu có điểm nằm trong vòng tròn bán kính 2m thì được xem là hàng xóm.

2. minPts
    Là số lượng hàng xóm tối thiểu để tạo thành một cụm.

    Ví dụ
        minPts = 5
            Muốn trở thành "điểm trung tâm" thì phải có ít nhất 5 điểm ở gần.
```
**DBSCAN chia điểm thành 3 loại.**
```bash
1. Core Point
    Có đủ hàng xóm.

    Ví dụ
          ●
       ●  ●  ●
          X
       ●
    X có rất nhiều điểm xung quanh. => Core Point.

2. Border Point
    Không đủ hàng xóm nhưng nằm cạnh một Core Point.

    Ví dụ
        ● ● ● ●

              ○
    ○ không đủ hàng xóm. Nhưng sát cluster. => Border Point.

3. Noise
    Không gần cluster nào.

                 x

    => Noise.
```
Ví dụ từng bước

Giả sử

eps = 1

minPts = 4

Có dữ liệu

A B C

D E F

G

E nhìn quanh thấy

A B C
D E F
G

Có 7 điểm.

=> E là Core.

Sau đó DBSCAN mở rộng.

Nếu F cũng là Core

A B C
D E F H I
G

Cluster tiếp tục lan rộng.

Nếu tới điểm

              Z

Không có ai gần.

=> Noise.

Thuật toán thực hiện

Pseudo code

for mỗi điểm:

    nếu đã thăm:
        bỏ qua

    tìm tất cả hàng xóm

    nếu hàng xóm < minPts:
        đánh dấu Noise

    ngược lại:
        tạo Cluster mới

        duyệt toàn bộ hàng xóm

            nếu hàng xóm cũng là Core

                mở rộng Cluster

Ý tưởng rất giống hiệu ứng "lây lan":

Core
 ↓
Core
 ↓
Core
 ↓
Core
 ↓
Border
Minh họa
Cluster A

● ● ●
● ● ●
 ● ●


Cluster B

         ● ●
       ● ● ●
        ●


Noise

               x

DBSCAN trả về

Cluster A

Cluster B

Noise
Ưu điểm

✅ Không cần biết trước có bao nhiêu cluster.

Khác với K-Means.

K-Means

k = 3

Phải nói trước.

DBSCAN

Tự tìm.

✅ Tìm được cluster hình dạng bất kỳ.

Ví dụ

*************
*
*
************

Hoặc

(((((((((((

DBSCAN vẫn gom đúng.

K-Means thường gặp khó với các cụm có hình dạng phức tạp.

✅ Phát hiện Noise rất tốt.

Ví dụ

Cluster

●●●●●

          x

                 y

x và y sẽ bị loại.

Nhược điểm

❌ Khó chọn eps.

Nếu quá nhỏ

● ● ●     ●

=> nhiều cluster nhỏ.

Nếu quá lớn

● ● ●      ● ●

=> gộp hết thành một cluster.

❌ Không tốt nếu mật độ các cluster quá khác nhau.

Ví dụ

Cluster 1

●●●●●●●●●●

Cluster 2

●     ●
   ●
      ●

Một cụm rất dày, cụm kia rất thưa. Một giá trị eps và minPts có thể không phù hợp cho cả hai.

So sánh với K-Means
K-Means	DBSCAN
Phải biết trước số cluster (k)	Không cần biết trước
Không phát hiện Noise	Có phát hiện Noise
Tốt với cluster hình tròn	Tốt với cluster có hình dạng bất kỳ
Nhanh trên dữ liệu lớn	Có thể chậm hơn khi dữ liệu rất lớn hoặc số chiều cao
Mỗi điểm đều thuộc một cluster	Có thể gán một số điểm là Noise
Khi nào nên dùng DBSCAN?

DBSCAN rất phù hợp khi bạn:

Muốn không cần chỉ định trước số lượng cụm.
Cần phát hiện các điểm ngoại lai (outliers/noise).
Dữ liệu có các cụm với hình dạng phức tạp, không chỉ là hình tròn.
Ví dụ thực tế:
Phát hiện khu vực tập trung khách hàng trên bản đồ GPS.
Gom nhóm vị trí taxi, xe giao hàng.
Phát hiện giao dịch bất thường trong dữ liệu tài chính.
Nhóm các điểm trong xử lý ảnh hoặc dữ liệu không gian.
Tóm tắt trực quan
Bước 1:
Chọn một điểm.

      ●

Bước 2:
Có đủ hàng xóm trong bán kính eps?

   ✔ Có  → Core Point → Tạo cluster.
   ✘ Không → Tạm đánh dấu Noise.

Bước 3:
Từ Core Point, tiếp tục mở rộng sang các Core Point lân cận.

      ● ● ●
    ● ● ● ●
      ● ●

Bước 4:
Không còn điểm nào có thể mở rộng → Hoàn thành cluster.

Lặp lại cho các điểm chưa được thăm.

Có thể hình dung DBSCAN như đổ một giọt mực lên các vùng có nhiều điểm: mực sẽ lan qua các điểm nằm đủ gần nhau để tạo thành một cụm, còn những điểm đứng riêng lẻ sẽ không được "nhuộm" và được xem là noise. Đây chính là ý tưởng cốt lõi giúp DBSCAN khác biệt so với nhiều thuật toán phân cụm khác.