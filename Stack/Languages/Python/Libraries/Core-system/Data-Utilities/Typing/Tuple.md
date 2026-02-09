# Tuple
```python
from typing import Tuple

def get_user() -> Tuple[int, str]:
    return (1, "Thắng")

user = get_user()
print(user)

# IDE sẽ hiểu tuple luôn có đúng 2 phần tử: int và str.
```