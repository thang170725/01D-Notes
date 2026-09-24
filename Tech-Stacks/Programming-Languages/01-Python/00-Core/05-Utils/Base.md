- [iter() (biến một object có thể lặp (list, dict, tuple, ...) thành iterator)](#iter-biến-một-object-có-thể-lặp-list-dict-tuple--thành-iterator)
- [next() (lấy phần tử tiếp theo từ iterator)](#next-lấy-phần-tử-tiếp-theo-từ-iterator)
---
# iter() (biến một object có thể lặp (list, dict, tuple, ...) thành iterator)
**Ex**
```python
a = [1,2,3,4,5]

it = iter(a)
print(it) # <list_iterator object at 0x000001A2525ED0F0>
```
# next() (lấy phần tử tiếp theo từ iterator)
**Syn**
```bash
n = next(iterator, default)

- Input:
    + default: Nếu iterator hết → trả về default thay vì báo StopIteration.
```
```python
data = [10, 20, 30]

it = iter(data)

x = next(it)
print(x) # 10
```