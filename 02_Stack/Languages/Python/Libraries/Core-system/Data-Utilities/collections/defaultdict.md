# Defaultdict
**Syn**
```python
from collections import defaultdict

class BFS:
    def __init__(self):
        self.data = defaultdict(list)

    def tree_data(self):
        # Khởi tạo dữ liệu cây dạng dictionary (adjacency list)
        self.data['A'] = ['B', 'C', 'D']
        self.data['B'] = ['M', 'N']
        self.data['C'] = ['L']
        self.data['D'] = ['O', 'P']
        self.data['M'] = ['X', 'Y']
        self.data['N'] = ['U', 'V']
        self.data['O'] = ['I', 'J']
        self.data['Y'] = ['R', 'S']
        self.data['V'] = ['G', 'H']
        return self.data

if __name__ == '__main__':
    bfs = BFS()
    print(bfs.tree_data())
# defaultdict(<class 'list'>, {'A': ['B', 'C', 'D'], 'B': ['M', 'N'], 'C': ['L'], 'D': ['O', 'P'], 'M': ['X', 'Y'], 'N': ['U', 'V'], 'O': ['I', 'J'], 'Y': ['R', 'S'], 'V': ['G', 'H']})
```