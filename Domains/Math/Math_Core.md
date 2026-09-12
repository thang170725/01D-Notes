- [Dijkstra's Algorithm (thuật toán dùng để tìm đường đi ngắn nhất)](#dijkstras-algorithm-thuật-toán-dùng-để-tìm-đường-đi-ngắn-nhất)
- [số chẵn và số lẻ](#số-chẵn-và-số-lẻ)
- [DFS](#dfs)
- [LeetCode 1038 - Medium](#leetcode-1038---medium)
- [Leetcode - 2181](#leetcode---2181)
---
# Dijkstra's Algorithm (thuật toán dùng để tìm đường đi ngắn nhất)
**Tư duy cốt lõi của Dijkstra**
```bash
Bước 1: Chọn node có distance nhỏ nhất
Bước 2: Thử đi qua các cạnh của nó
    Ví dụ:
        - A → C = 3
        - C → B = 2

    thì thử: distance[C] + 2 = 3 + 2 = 5
Bước 3: Nếu đường mới tốt hơn thì cập nhật
```
**Dijkstra đang được ứng dụng ở đâu?**
```bash
🗺️ GPS / bản đồ
🌐 Network routing
    Hãy tưởng tượng Internet:

Router A
   |
   +---- Router B
   |
   +---- Router C
            |
            +---- Router D

Mỗi connection có một cost.

Routing algorithm cần tìm:

A → D

theo đường có cost thấp nhất.

Một ví dụ kinh điển là OSPF (Open Shortest Path First), sử dụng thuật toán shortest-path dựa trên Dijkstra để tính đường đi trong một mạng.

🎮 Game

Trong game:

Player
   ↓
Map

NPC cần tìm đường:

S → → → → → E

Mỗi ô có thể có cost:

Road       = 1
Grass      = 2
Mud        = 5
Mountain   = 10

Dijkstra có thể tìm:

Đường có tổng cost nhỏ nhất, chứ không nhất thiết ít ô nhất.

10. Một ví dụ rất hay để hiểu bản chất

Giả sử bạn đi từ A đến D.

       1
   A ------ B
   |        |
  10        1
   |        |
   C ------ D
       1

Có hai đường:

Đường 1
A → C → D

10 + 1 = 11
Đường 2
A → B → D

1 + 1 = 2

Dijkstra tìm được:

A → B → D

Không phải vì nó có ít node hơn, mà vì:

TOTAL COST = 2

Đây chính là bản chất của shortest path.

11. Dijkstra khác BFS ở đâu?

Đây là câu hỏi phỏng vấn rất hay.

BFS
A
├── B
├── C
└── D

Mỗi bước coi như cost:

1

BFS tìm:

Ít cạnh nhất.

Dijkstra
A --100--> B
A --1----> C
C --1----> B

BFS có thể thích:

A → B

vì chỉ 1 cạnh.

Nhưng Dijkstra thấy:

A → C → B
= 1 + 1
= 2

tốt hơn:

A → B
= 100

Nên:

BFS tối ưu số bước.
Dijkstra tối ưu tổng trọng số.

12. Một điểm rất quan trọng: tại sao Dijkstra hoạt động?

Đây là insight thuật toán mà bạn nên hiểu thay vì chỉ học thuộc code.

Giả sử Dijkstra chọn:

A → C

với:

distance[C] = 5

và C là node chưa xử lý có khoảng cách nhỏ nhất.

Vì mọi edge đều có weight ≥ 0, nên nếu đi vòng qua một node khác trước khi đến C:

A → X → ... → C

thì tổng cost không thể tự nhiên giảm xuống dưới 5.

Do đó, khi Dijkstra chọn node có distance nhỏ nhất, nó có thể chốt khoảng cách đó.

Đây chính là lý do điều kiện:

weight >= 0

quan trọng đến vậy.

13. Nếu học DSA, bạn nên nhớ Dijkstra theo flow này

Đừng học thuộc code trước. Hãy nhớ:

        Graph
          │
          ▼
Có trọng số?
     /          \
   No            Yes
   │              │
   ▼              ▼
  BFS       Weight có âm?
                  /   \
                Yes    No
                 │      │
                 ▼      ▼
          Bellman-Ford Dijkstra

Và bản thân Dijkstra:

distance[start] = 0
distance[others] = ∞

        ↓

Chọn node chưa xử lý
có distance nhỏ nhất

        ↓

Relax tất cả hàng xóm

        ↓

Có đường mới tốt hơn?
        │
       Yes
        ↓
Update distance

        ↓

Lặp lại

Nếu bạn đang học LeetCode, Dijkstra là một thuật toán rất đáng học sau BFS/DFS. Đặc biệt, khi gặp đề có các cụm như "minimum cost", "shortest time", "minimum distance", "weighted graph", bạn nên lập tức nghĩ đến Dijkstra (sau đó kiểm tra xem có trọng số âm hay không).
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