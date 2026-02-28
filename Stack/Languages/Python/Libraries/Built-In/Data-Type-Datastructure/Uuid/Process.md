- [uuid4()](#uuid4)
- [uuid1()](#uuid1)
- [uuid3()](#uuid3)
- [uuid5()](#uuid5)
---
# uuid4()
```bash
Tạo ID ngẫu nhiên (random) — dùng nhiều nhất
```
**Ex**
```python
import uuid

id = uuid.uuid4()
print(id) # 3f50c9a4-9f4d-4d1c-9d7c-82fbe7bfa123
```
# uuid1()
```bash 
- Dựa trên thời gian + MAC address
- Có thể truy ra thời điểm tạo → ít dùng hơn nếu cần bảo mật.
```
**Ex**
```python
import uuid

print(uuid.uuid1())
```
# uuid3() 
```bash
- Dựa trên namespace + tên (MD5)
- Cùng input → luôn ra cùng 1 UUID
```
**Ex**
```python
import uuid

print(uuid.uuid3(uuid.NAMESPACE_DNS, "example.com"))
```
# uuid5() 
```bash
giống uuid3 nhưng dùng SHA-1
```
**Ex**
```python
import uuid

print(uuid.uuid5(uuid.NAMESPACE_DNS, "example.com"))
```