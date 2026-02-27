- [Random](#random)
  - [.random()](#random-1)
  - [.seed()](#seed)
  - [Randint()](#randint)
  - [.uniform()](#uniform)
---
# Random
```bash
- Để tạo ra số ngẫu nhiên.
- Cách tạo số từ min đến max: min + rand()%(max-min+1) - rand() phải chạy từ 0 đến 1
```
## .random()
```bash
Để tạo ra một số thực từ 0 đến 1.
```
## .seed()
**Ex**
```python
rnd.seed(1)
for i in range(3):
    random = int(20 + rnd.random()*(30 - 20 + 1))
    print(random)

# kết quả khi chạy lần 1
21
29
28
# kết quả khi chạy lần 2
21
29
28
```
## Randint()
```bash
Để tạo ra một số ngẫu nhiên nguyên trong phạm vi từ x đến y.
```
**Syn**
```bash
random.randint(start, end)  # sinh ra số ngẫu nhiên từ start đến end
```
## .uniform()
```bash
Tạo ra số thực trong phạm vi từ x đến y.
```
**Syn**
```bash
Random.uniform(start, end) # sinh ra số ngẫu nhiên từ start đến end
```
## .gauss
```bash
tạo số ngẫu nhiên theo phân phối chuẩn (Gaussian distribution).
```
**Syn**
```bash
import random

random.gauss(mu, sigma)

- mu → giá trị trung bình (mean)
- sigma → độ lệch chuẩn (standard deviation)
```
**Ex**
```python
import random

x = random.gauss(0, 1)
print(x)
```