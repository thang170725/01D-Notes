- [tqdm()](#tqdm)
---
# tqdm()
**Syn**
```bash
from tqdm import tqdm
for i in tqdm(interable, des):
    ...

- Input:
    + des   : mô tả tiến trình
```
**Ex: tính tổng list có thanh tiến trình**
```python
from tqdm import tqdm
import time

li = [1,2,3,4]
res = 0
for i in tqdm(li, desc="Calc Sum List"):
    res += i
    time.sleep(0.5) 
print(res)
# Calc Sum List: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4/4 [00:02<00:00,  1.99it/s]
# 10
```
