# DFS
```python
from collections import defaultdict

class DFS:
    def __init__(self):
        self.data = defaultdict(list)
        self.tree_data()

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

    def dfs_path(self, start, end, path=None):
        """
        Tìm một đường từ start đến end bằng DFS (đệ quy).
        Trả về list các nút theo đường tìm được hoặc None nếu không tìm thấy.
        """
        if path is None:
            path = []

        # tạo bản sao đường đi hiện tại + thêm nút start
        path = path + [start]

        if start == end:
            return path

        # Nếu start không tồn tại trong đồ thị (không có kề) -> None
        if start not in self.data:
            return None

        for neighbor in self.data[start]:
            if neighbor not in path:  # tránh vòng lặp
                new_path = self.dfs_path(neighbor, end, path)
                print(neighbor, new_path)
                if new_path:
                    return new_path

        return None
    
if __name__ == '__main__':
    dfs = DFS()

    p = dfs.dfs_path('A', 'R')
    print("DFS path:", " -> ".join(p) if p else "No path")
```
# LeetCode 1038 - Medium
```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution(object):
    def bstToGst(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: Optional[TreeNode]
        """
        self.sum = 0

        def dfs(node):
            if not node:
                return

            # đi sang phải
            dfs(node.right)

            # xử lý node
            self.sum += node.val
            node.val = self.sum

            # di sang trái
            dfs(node.left)
        
        dfs(root)
        return root
```