# Dict 
```python
from typing import Dict

def count_words(words: List[str]) -> Dict[str, int]:
    counts = {}
    for w in words:
        counts[w] = counts.get(w, 0) + 1
    return counts

print(count_words(["a", "b", "a"]))

# IDE sẽ gợi ý rằng key là str, value là int.
```
# List
```python
from typing import List

def sum_list(numbers: List[int]) -> List[int]:
    return numbers

print(sum_list([1, 2, 3]))          # truyền đúng -> không lỗi
print(sum_list(["a", "b", "c"]))    # truyền sai -> không lỗi

# Chỉ dùng để gợi ý cho IDE không gây lỗi runtime dù có truyền sai
```