# Sắp xếp danh sách sự kiện
```bash
# cột 1 là địa điểm, cột 2 là số lượng khách.
data = {
    'event1': ['hanoi', 30],
    'event2': ['hanoi', 10],
    'event3': ['hanoi', 40],
    'event4': ['hanoi', 35],
}
```
```python
sorted_data = dict(
    sorted(data.items(), key=lambda item: item[1][1])
)
```