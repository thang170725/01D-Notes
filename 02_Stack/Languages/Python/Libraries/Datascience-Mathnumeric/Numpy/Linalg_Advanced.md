# norm()
```bash
- Thường được dùng để tính khoảng cách hai điểm trong không gian.
```
**Ex**
```python
import numpy as np

# Tạo một mảng chứa tọa độ của 3 điểm: (3,4), (1,1), và (0,5)
points = np.array([
    [3, 4],
    [1, 1],
    [0, 5]
])

# Tính L2 norm (khoảng cách Euclidean) theo từng hàng (axis=1)
distances = np.linalg.norm(points, axis=1)

print("Các điểm:")
print(points)
print("\nKhoảng cách từ gốc tọa độ đến mỗi điểm:")
print(distances)
Các điểm:
[[3 4]
 [1 1]
 [0 5]]

Khoảng cách từ gốc tọa độ đến mỗi điểm:
[5.         1.41421356 5.        ]
```
# Tính khoảng cách 2 điểm trong không gian 2d
```python
import numpy as np

coordinates = np.array([
    [1,2],
    [3,4]
])

distance = np.linalg.norm(coordinates[0]-coordinates[1])
print(distance) # 2.8284271247461903
```