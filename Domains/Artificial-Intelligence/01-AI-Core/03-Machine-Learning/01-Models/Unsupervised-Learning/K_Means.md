- [Introduction](#introduction)
- [Practices](#practices)
  - [Demo code thuần thuật toán K-Mean](#demo-code-thuần-thuật-toán-k-mean)
---
# Introduction
```bash
- K-Means là một trong những thuật toán clustering (phân cụm) nổi tiếng nhất.
    + Khác với Linear Regression hay Classification:
        - Không có nhãn (label)
        - Không biết trước dữ liệu thuộc nhóm nào

Nhiệm vụ của K-Means là:
    "Tự động chia dữ liệu thành K nhóm sao cho các điểm trong cùng nhóm giống nhau nhất có thể."

Ý tưởng cốt lõi
    Giả sử chọn: K=2
        tức muốn chia thành 2 cụm.
    K-Means sẽ:
        1. Chọn 2 tâm cụm (centroid) ban đầu
        2. Gán mỗi điểm vào tâm gần nhất
        3. Tính lại tâm cụm
        4. Lặp lại đến khi không thay đổi nữa
```
**Ex**
```bash
Giả sử bạn có dữ liệu khách hàng:
| Khách hàng | Thu nhập |
| ---------- | -------- |
| A          | 10       |
| B          | 12       |
| C          | 15       |
| D          | 100      |
| E          | 105      |
| F          | 110      |

Nhìn bằng mắt:
    10 12 15          100 105 110
Rõ ràng có 2 nhóm:
    - Nhóm thu nhập thấp
    - Nhóm thu nhập cao
K-Means sẽ tự tìm ra điều này.
```
**Ex: Ví dụ chi tiết**
```bash
Dữ liệu:
    10, 12, 15, 100, 105, 110
Muốn: K=2
```
```bash
Bước 1: Chọn centroid ngẫu nhiên
    Giả sử:
        C1 = 12
        C2 = 105
Bước 2: Gán điểm vào centroid gần nhất
    Tính khoảng cách.
        Điểm 10
            Đến C1: ∣10−12∣=2
            Đến C2: ∣10−105∣=95
            → thuộc cụm 1
        Điểm 15
            Đến C1: ∣15−12∣=3
            Đến C2: ∣15−105∣=90
            → cụm 1
        Điểm 100
            Đến C1: ∣100−12∣=88
            Đến C2: ∣100−105∣=5
            → cụm 2

    Kết quả:
        Cluster 1:
        10 12 15

        Cluster 2:
        100 105 110
Bước 3: Tính centroid mới
    Centroid = trung bình các điểm trong cụm.
        Cluster 1: 10 12 15
            Trung bình:(10+12+15)/3 = 12.33
        Cluster 2: 100 105 110
            Trung bình: (100+105+110)/3 = 105
    Centroid mới:
        C1 = 12.33
        C2 = 105
Bước 4: Gán lại
    Tính lại khoảng cách.
    Kết quả không đổi: 
        10 12 15
            vẫn thuộc Cluster 1
        100 105 110
            vẫn thuộc Cluster 2

Thuật toán dừng.
```
# Practices
## Demo code thuần thuật toán K-Mean
```python
import math
from typing import List, Tuple, Any

class KMeansResearch:
    def __init__(self, 
        data: List[Tuple[int, int]],              # list of tuple coordinates of dataset [(1,2), (3,4), ...]
        initial_centroids: List[Tuple[int, int]]  # list of tuple of coordinates of the center [(1,1), (2,2), ...]
    ) -> Any:
        self.data = data  
        self.centroids = initial_centroids.copy()
     
        self.k = len(initial_centroids)
        self.clusters = [[] for _ in range(self.k)]  # Lưu các điểm thuộc mỗi cụm

        print("=== BƯỚC 0: KHỞI TẠO THUẬT TOÁN K-MEANS ===")
        print(f"Tổng số điểm dữ liệu: {len(data)}")
        for i, pt in enumerate(data):
            print(f"  x{i+1} = {pt}")
        print("\nTâm cụm ban đầu được chọn:")
        for i, c in enumerate(self.centroids):
            print(f"  Tâm m{i+1} = {c}")
        print("-" * 60)

    def _euclidean_distance(self, 
        pt1: Tuple[int, int], 
        pt2: tuple[int, int]
    ):
        """Tính khoảng cách Euclid giữa 2 điểm trong không gian 2D."""
        return math.sqrt((pt1[0] - pt2[0]) ** 2 + (pt1[1] - pt2[1]) ** 2)

    def fit(self, max_iterations=10):
        """Chạy vòng lặp cập nhật tâm cụm cho đến khi hội tụ."""

        for iteration in range(max_iterations):
            print(f"\n🔄 VÒNG LẶP (ITERATION) THỨ {iteration + 1}:")

            # 1. Reset lại danh sách các điểm trong cụm của vòng lặp cũ
            new_clusters = [[] for _ in range(self.k)]

            # 2. Bước gán cụm (Assignment Step)
            print("  [Bước 2.1: Tính khoảng cách và Gán cụm]")
            for i, pt in enumerate(self.data):
                distances = []
                for c_idx, centroid in enumerate(self.centroids):
                    dist = self._euclidean_distance(pt, centroid)
                    distances.append(dist)

                # Tìm tâm cụm gần điểm này nhất
                min_dist_idx = distances.index(min(distances))
                new_clusters[min_dist_idx].append(pt)

                # Log chi tiết khoảng cách của từng điểm đến 3 tâm
                dist_str = ", ".join(
                    [f"đến m{j+1}: {d:.2f}" for j, d in enumerate(distances)]
                )
                print(
                    f"    Điểm x{i+1}{pt}: {dist_str} => Thuộc cụm C{min_dist_idx+1}"
                )

            # In tổng kết các cụm sau khi gán xong
            print("\n  -> Kết quả gom cụm tạm thời:")
            for c_idx, cluster in enumerate(new_clusters):
                print(f"     Cụm C{c_idx+1}: {cluster}")

            # 3. Bước cập nhật tâm cụm (Update Step)
            print("\n  [Bước 2.2: Cập nhật lại tọa độ tâm cụm (Tính trung bình cộng)]")
            new_centroids = []
            for c_idx, cluster in enumerate(new_clusters):
                if len(cluster) == 0:
                    # Nếu cụm không có điểm nào, giữ nguyên tâm cũ để tránh lỗi chia cho 0
                    new_centroids.append(self.centroids[c_idx])
                    print(
                        f"     Cụm C{c_idx+1} rỗng! Giữ nguyên tâm m{c_idx+1} = {self.centroids[c_idx]}"
                    )
                    continue

                # Tính trung bình cộng tọa độ X và Y của tất cả các điểm trong cụm
                sum_x = sum(pt[0] for pt in cluster)
                sum_y = sum(pt[1] for pt in cluster)
                mean_x = round(sum_x / len(cluster), 2)
                mean_y = round(sum_y / len(cluster), 2)
                new_centroid = (mean_x, mean_y)
                new_centroids.append(new_centroid)

                print(
                    f"     Tâm mới m{c_idx+1} = Trung bình của {cluster} = ({sum_x}/{len(cluster)}, {sum_y}/{len(cluster)}) = {new_centroid}"
                )

            # 4. Kiểm tra điều kiện dừng (Nếu tâm cụm không đổi nữa thì dừng)
            if new_centroids == self.centroids:
                print(
                    f"\n✅ THUẬT TOÁN HỘI TỤ TẠI VÒNG LẶP THỨ {iteration + 1}!"
                )
                self.clusters = new_clusters
                break

            # Cập nhật lại tâm cụm cho vòng lặp tiếp theo
            self.centroids = new_centroids
            print("-" * 60)

        return self.centroids, self.clusters


# --- CHẠY THỬ NGHIỆM VỚI SỐ LIỆU ĐỀ BÀI ---
if __name__ == "__main__":
    # Chuẩn hóa dữ liệu đầu vào từ đề bài
    X = [(1, 1), (1, 3), (2, 2), (4, 4), (4, 5), (5, 4), (5, 5)]

    # Tâm cụm ban đầu m1 = x1, m2 = x2, m3 = x3
    m1 = (1, 1)
    m2 = (1, 3)
    m3 = (2, 2)
    initial_m = [m1, m2, m3]

    # Khởi chạy quy trình research workflow
    kmeans = KMeansResearch(data=X, initial_centroids=initial_m)
    final_centroids, final_clusters = kmeans.fit()

    print("\n==================== KẾT QUẢ CUỐI CÙNG ====================")
    for i in range(len(final_centroids)):
        print(f"Cụm {i+1}: Tâm = {final_centroids[i]} | Các điểm = {final_clusters[i]}")
```
```bash
=== BƯỚC 0: KHỞI TẠO THUẬT TOÁN K-MEANS ===
Tổng số điểm dữ liệu: 7
  x1 = (1, 1)
  x2 = (1, 3)
  x3 = (2, 2)
  x4 = (4, 4)
  x5 = (4, 5)
  x6 = (5, 4)
  x7 = (5, 5)

Tâm cụm ban đầu được chọn:
  Tâm m1 = (1, 1)
  Tâm m2 = (1, 3)
  Tâm m3 = (2, 2)
------------------------------------------------------------

🔄 VÒNG LẶP (ITERATION) THỨ 1:
  [Bước 2.1: Tính khoảng cách và Gán cụm]
    Điểm x1(1, 1): đến m1: 0.00, đến m2: 2.00, đến m3: 1.41 => Thuộc cụm C1
    Điểm x2(1, 3): đến m1: 2.00, đến m2: 0.00, đến m3: 1.41 => Thuộc cụm C2
    Điểm x3(2, 2): đến m1: 1.41, đến m2: 1.41, đến m3: 0.00 => Thuộc cụm C3
    Điểm x4(4, 4): đến m1: 4.24, đến m2: 3.16, đến m3: 2.83 => Thuộc cụm C3
    Điểm x5(4, 5): đến m1: 5.00, đến m2: 3.61, đến m3: 3.61 => Thuộc cụm C2
    Điểm x6(5, 4): đến m1: 5.00, đến m2: 4.12, đến m3: 3.61 => Thuộc cụm C3
    Điểm x7(5, 5): đến m1: 5.66, đến m2: 4.47, đến m3: 4.24 => Thuộc cụm C3

  -> Kết quả gom cụm tạm thời:
     Cụm C1: [(1, 1)]
     Cụm C2: [(1, 3), (4, 5)]
     Cụm C3: [(2, 2), (4, 4), (5, 4), (5, 5)]

  [Bước 2.2: Cập nhật lại tọa độ tâm cụm (Tính trung bình cộng)]
     Tâm mới m1 = Trung bình của [(1, 1)] = (1/1, 1/1) = (1.0, 1.0)
     Tâm mới m2 = Trung bình của [(1, 3), (4, 5)] = (5/2, 8/2) = (2.5, 4.0)
     Tâm mới m3 = Trung bình của [(2, 2), (4, 4), (5, 4), (5, 5)] = (16/4, 15/4) = (4.0, 3.75)
------------------------------------------------------------

🔄 VÒNG LẶP (ITERATION) THỨ 2:
  [Bước 2.1: Tính khoảng cách và Gán cụm]
    Điểm x1(1, 1): đến m1: 0.00, đến m2: 3.35, đến m3: 4.07 => Thuộc cụm C1
    Điểm x2(1, 3): đến m1: 2.00, đến m2: 1.80, đến m3: 3.09 => Thuộc cụm C2
    Điểm x3(2, 2): đến m1: 1.41, đến m2: 2.06, đến m3: 2.66 => Thuộc cụm C1
    Điểm x4(4, 4): đến m1: 4.24, đến m2: 1.50, đến m3: 0.25 => Thuộc cụm C3
    Điểm x5(4, 5): đến m1: 5.00, đến m2: 1.80, đến m3: 1.25 => Thuộc cụm C3
    Điểm x6(5, 4): đến m1: 5.00, đến m2: 2.50, đến m3: 1.03 => Thuộc cụm C3
    Điểm x7(5, 5): đến m1: 5.66, đến m2: 2.69, đến m3: 1.60 => Thuộc cụm C3

  -> Kết quả gom cụm tạm thời:
     Cụm C1: [(1, 1), (2, 2)]
     Cụm C2: [(1, 3)]
     Cụm C3: [(4, 4), (4, 5), (5, 4), (5, 5)]

  [Bước 2.2: Cập nhật lại tọa độ tâm cụm (Tính trung bình cộng)]
     Tâm mới m1 = Trung bình của [(1, 1), (2, 2)] = (3/2, 3/2) = (1.5, 1.5)
     Tâm mới m2 = Trung bình của [(1, 3)] = (1/1, 3/1) = (1.0, 3.0)
     Tâm mới m3 = Trung bình của [(4, 4), (4, 5), (5, 4), (5, 5)] = (18/4, 18/4) = (4.5, 4.5)
------------------------------------------------------------

🔄 VÒNG LẶP (ITERATION) THỨ 3:
  [Bước 2.1: Tính khoảng cách và Gán cụm]
    Điểm x1(1, 1): đến m1: 0.71, đến m2: 2.00, đến m3: 4.95 => Thuộc cụm C1
    Điểm x2(1, 3): đến m1: 1.58, đến m2: 0.00, đến m3: 3.81 => Thuộc cụm C2
    Điểm x3(2, 2): đến m1: 0.71, đến m2: 1.41, đến m3: 3.54 => Thuộc cụm C1
    Điểm x4(4, 4): đến m1: 3.54, đến m2: 3.16, đến m3: 0.71 => Thuộc cụm C3
    Điểm x5(4, 5): đến m1: 4.30, đến m2: 3.61, đến m3: 0.71 => Thuộc cụm C3
    Điểm x6(5, 4): đến m1: 4.30, đến m2: 4.12, đến m3: 0.71 => Thuộc cụm C3
    Điểm x7(5, 5): đến m1: 4.95, đến m2: 4.47, đến m3: 0.71 => Thuộc cụm C3

  -> Kết quả gom cụm tạm thời:
     Cụm C1: [(1, 1), (2, 2)]
     Cụm C2: [(1, 3)]
     Cụm C3: [(4, 4), (4, 5), (5, 4), (5, 5)]

  [Bước 2.2: Cập nhật lại tọa độ tâm cụm (Tính trung bình cộng)]
     Tâm mới m1 = Trung bình của [(1, 1), (2, 2)] = (3/2, 3/2) = (1.5, 1.5)
     Tâm mới m2 = Trung bình của [(1, 3)] = (1/1, 3/1) = (1.0, 3.0)
     Tâm mới m3 = Trung bình của [(4, 4), (4, 5), (5, 4), (5, 5)] = (18/4, 18/4) = (4.5, 4.5)

✅ THUẬT TOÁN HỘI TỤ TẠI VÒNG LẶP THỨ 3!

==================== KẾT QUẢ CUỐI CÙNG ====================
Cụm 1: Tâm = (1.5, 1.5) | Các điểm = [(1, 1), (2, 2)]
Cụm 2: Tâm = (1.0, 3.0) | Các điểm = [(1, 3)]
Cụm 3: Tâm = (4.5, 4.5) | Các điểm = [(4, 4), (4, 5), (5, 4), (5, 5)]
```