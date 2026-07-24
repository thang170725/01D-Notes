- [Fenwick Tree (là một cấu trúc dữ liệu dùng để cập nhật giá trị của một phần tử trong mảng)](#fenwick-tree-là-một-cấu-trúc-dữ-liệu-dùng-để-cập-nhật-giá-trị-của-một-phần-tử-trong-mảng)
- [số chẵn và số lẻ](#số-chẵn-và-số-lẻ)
- [DFS](#dfs)
- [LeetCode 1038 - Medium](#leetcode-1038---medium)
- [Leetcode - 2181](#leetcode---2181)
---
# Fenwick Tree (là một cấu trúc dữ liệu dùng để cập nhật giá trị của một phần tử trong mảng)
```bash
Tính tổng tiền tố (Prefix Sum) rất nhanh.
    Thay vì:
        - Update: O(1)
        - Query tổng từ 0 -> i: O(n)
    thì Fenwick Tree cho phép:
        - Update: O(log n)
        - Query Prefix Sum: O(log n)
```
**Ý tưởng**
```bash
Giả sử bạn có mảng:
    Index:  1  2  3  4  5
    Value:  2  1  3  5  4

Bạn cần thực hiện rất nhiều câu hỏi kiểu:
    Tổng từ phần tử 1 đến phần tử i là bao nhiêu?

Ví dụ:
    - sum(3) = 2 + 1 + 3 = 6
    - sum(5) = 2 + 1 + 3 + 5 + 4 = 15

Cách bình thường
    Mỗi lần hỏi:
        sum(5)
            bạn sẽ cộng: 2 + 1 + 3 + 5 + 4
        => phải đi qua 5 số.
        => Nếu có 100.000 số thì phải cộng 100.000 lần. = Rất chậm.

Ý tưởng của Fenwick Tree
    Thay vì mỗi lần cộng lại từ đầu. Ta lưu sẵn một số tổng. -> Nó giống như bạn ghi nhớ sẵn các tổng để sau này dùng lại.

    Giả sử cần tính sum(4)
        Thay vì: 2 + 1 + 3 + 5

        Fenwick Tree biết rằng tree[4] đã bằng 11 => lấy luôn.

    Ví dụ khác
        Muốn tính sum(6)

        Giả sử mảng là 2 1 3 5 4 6
            Fenwick Tree không cộng: 2+1+3+5+4+6
            
            Nó lấy: tree[6] + tree[4] vì tree[6] đã chứa 4+6 và tree[4] đã chứa 2+1+3+5
                => Tổng là (4+6) + (2+1+3+5) # Không cần cộng từng số nữa.
```
# số chẵn và số lẻ
**Công thức tổng n số lẻ đầu tiên**
```bash
s = n**2

chứng minh:
    S=(2⋅1−1)+(2⋅2−1)+⋯+(2⋅n−1)
    S=2(1+2+⋯+n)−n
    S=2*(n(n+1))/2 − n
     =n(n+1)−n
     =n**2
```
**Công thức tổng n số chẵn đầu tiên**
```bash
s = n*(n+1)

chứng minh:
    s = 2 + 4 + 6 + ... + 2n
      = 2*(1+2+...+n) = 2*(n(n+1))/2 = n*(n+1)
```
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
- [Leetcode - 2181](#leetcode---2181)
---
# Leetcode - 2181
**Ex1**
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeNodes(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        new_head = ListNode(0)
        tail = new_head
        temp = head.next
        s = 0
        while temp:
            if temp.val == 0:
                new_node = ListNode(val=s)
                tail.next = new_node
                tail = new_node
                s = 0
            else:
                s += temp.val
            temp = temp.next
        
        return new_head.next
```
**Ex2**
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeNodes(self, head):
        """
        :type head: Optional[ListNode]
        :rtype: Optional[ListNode]
        """
        cur = head
        temp = head.next
        s = 0

        while temp:
            if temp.val == 0:
                cur = cur.next
                cur.val = s
                s = 0
            else:
                s += temp.val
            temp = temp.next
        
        cur.next = None
        return head.next
```