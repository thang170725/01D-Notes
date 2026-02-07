# Tạo cột flag
**Ex**
```python
import pandas as pd

df = pd.DataFrame({
    'name': ['A', 'B', 'C', 'D'],
    'age': [15, 16, -2, 14],
    'score': [80, 120, 60, 90]
})

df['invalid_age'] = (
    (df['age'] < 5) | (df['age'] > 18)
).astype(int)

# name   age   score   invalid_age
# A      15    80      0
# B      16    120     0
# C      -2    60      1
# D      14    90      0
```
