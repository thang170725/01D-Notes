+ [<<Back](../Base.md)
- [Recursion (Đệ quy)](#recursion-đệ-quy)
  - [Practices](#practices)
    - [Tìm phần tử thứ n trong dãy fibonaci](#tìm-phần-tử-thứ-n-trong-dãy-fibonaci)
- [Dijkstra's Algorithm (thuật toán dùng để tìm đường đi ngắn nhất)](#dijkstras-algorithm-thuật-toán-dùng-để-tìm-đường-đi-ngắn-nhất)
- [Fenwick Tree (là một cấu trúc dữ liệu dùng để cập nhật giá trị của một phần tử trong mảng)](#fenwick-tree-là-một-cấu-trúc-dữ-liệu-dùng-để-cập-nhật-giá-trị-của-một-phần-tử-trong-mảng)
- [số chẵn và số lẻ](#số-chẵn-và-số-lẻ)
- [DFS](#dfs)
- [Binary Tree](#binary-tree)
  - [Practices](#practices-1)
- [LeetCode 1038 - Medium](#leetcode-1038---medium)
- [Leetcode - 2181](#leetcode---2181)
- [Thuật toán tìm ước chung lớn nhất](#thuật-toán-tìm-ước-chung-lớn-nhất)
- [Tìm UCLN](#tìm-ucln)
- [Thuật toán Backtracking (Quay lui)](#thuật-toán-backtracking-quay-lui)
  - [Practices](#practices-2)
    - [Sinh dãy nhị phân có n phần tử](#sinh-dãy-nhị-phân-có-n-phần-tử)
---
# Recursion (Đệ quy)
## Practices
### Tìm phần tử thứ n trong dãy fibonaci
```c++
#include <iostream>
using namespace std;
int fibonaci(int n){// n = 0,1,2,...
    if(n==0 || n==1) return 1;
    return fibonaci(n-1) + fibonaci(n-2);
}
int main(){
    cout << fibonaci(4);
    return 0;
}
5
```
Tìm phần tử thứ n trong dãy fibonaci có nhớ
#include <iostream>
#include <vector>
using namespace std;

// Hàm đệ quy có nhớ
long long fib(int n, vector<long long> &memo) {
    // Trường hợp cơ sở
    if (n <= 1) return n;

    // Nếu đã tính rồi, trả về ngay
    if (memo[n] != -1) return memo[n];

    // Ngược lại, tính và lưu lại
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
}

int main() {
    int n;
    cout << "Nhap n: ";
    cin >> n;

    // Khởi tạo mảng nhớ, gán -1 (chưa tính)
    vector<long long> memo(n + 1, -1);

    cout << "So Fibonacci thu " << n << " la: " << fib(n, memo);
    return 0;
}
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
```
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
# Binary Tree
## Practices
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
# Thuật toán tìm ước chung lớn nhất
**phương pháp vòng lặp và điều kiện**
```bash
Với a = 18, b = 12
    Ý tưởng: Lặp từ 1 -> min(18, 12)
    - Loop 1: 
```
**phương pháp gcd**
*python*
```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a
# a = 18, b = 12 
# Loop 1: a = 18, b = 12 -> a = 12, b = 6
# Loop 2: a = 12, b = 6 -> a = 6, b = 0 (dừng) -> return a = 6
```
# Tìm UCLN
**Ex1**
```python
def UCLN(n1,n2):
    result = 1
    
    while n1 % 2 == 0  and n2 % 2 == 0: # xử lý riêng trường hợp 2 số đó chia hết cho 2 (chẵn)
        n1 //= 2
        n2 //= 2
        result *= 2
    # xử lý các trường hợp còn lại (lẻ)
    for i in range(3, min(n1,n2)+1, 2):
        while n1 % i == 0 and n2 % i == 0:
            n1 /= i
            n2 /= i
            result *= i
    return result
def main():
    print(UCLN(12, 18))
main()
```
**Ex2: Cải tiến code**
```python
def UCLN(n1,n2):
    while n2 != 0:
        r = n1 % n2
        n1 = n2
        n2 = r
    return n1
def main():
    print(UCLN(12, 18))
main()
```
**Ex3: Bằng hàm đệ quy**
```python
def UCLN(n1,n2,result = 1):
    if(n1 == 1 or n2 == 1): return 1
    # xử lý riêng trường hợp 2 số đó chia hết cho 2 (chẵn)
    while n1 % 2 == 0  and n2 % 2 == 0:
        return UCLN(n1//2, n2//2, result*2)
    # xử lý các trường hợp còn lại (lẻ)
    i = 3
    while i <= min(n1,n2):
        if n1 % i == 0 and n2 % i == 0:
            return UCLN(n1//i, n2//i, result*i)
        i += 2
    return result
def main():
    print(UCLN(22, 18))
main()
```

**Ex: Cải tiến code**
```python
def UCLN(n1,n2):
    if n2 == 0:
        return n1
    return UCLN(n2, n1 % n2)
def main():
    print(UCLN(22, 18))
main()
```
# Thuật toán Backtracking (Quay lui) 
## Practices
### Sinh dãy nhị phân có n phần tử
**Ex**
```c++
#include <iostream>
using namespace std;

void sinh_nhi_phan_2(int n, string current){
    if (current.length() == n){
        cout << current << endl;
        return;
    }
    string current1 = current+"0";
    string current2 = current+"1";
    sinh_nhi_phan_2(n, current1);
    sinh_nhi_phan_2(n, current2);
}

int main(){
    int n = 3;
    int x[n+1];
    sinh_nhi_phan_2(n, x);
    return 0;
}
// 000
// 001
// 010
// 011
// 100
// 101
// 110
// 111
```
#include <iostream>
using namespace std;

void print(int x[], int n){
    for(int i = 1; i <= n; i++){
        cout << x[i];
    }
    cout << endl;
}

void truy(int x[], int index, int n){
    for(int i = 0; i <= 1; i++){
        x[index] = i;
        if(index == n){
            print(x, n);
        }
        else{
            truy(x, index+1, n);
        }
    }
}

int main(){
    int n = 3;
    int x[n+1];
    truy(x, 1, 3);
    return 0;
}
000
001
010
011
100
101
110
111
Sinh tổ hợp chập k của n bằng quay lui
#include <iostream>
using namespace std;

void print(int x[], int k){
    for(int i = 1; i <= k; i++){
        cout << x[i];
    }
    cout << endl;
}

void truy(int x[], int index, int n, int k){
    for(int i = x[index-1]+1; i <= n-k+index; i++){
        x[index] = i; 
        if(index == k){
            print(x, k);
        }
        else{
            truy(x, index+1, n, k);
        }
    }
}

int main(){
    int n = 6;
    int k = 3;
    int x[n+1];
    x[0] = 0;
    truy(x, 1, n, k);
    return 0;
}
123
124
125
126
134
135
136
145
146
156
234
235
236
245
246
256
345
346
356
356
356
456
Chia để trị
Bài tập
Tìm giá trị lớn nhất trong mảng bằng chia để trị
int max_value(int x[], int l, int r){
    if (l==r){
        return x[l];
    }
    else{
        int m = (int)((l+r)/2);
        int max_left = max_value(x, l, m);
        int max_right = max_value(x, m+1, r);

        return max(max_left, max_right);
    }
}
Tìm giá trị chẵn nhỏ nhất trong mảng bằng chia để trị
#include <iostream>
#include <climits>
using namespace std;

int min_even_value(int x[], int l, int r){
    if (l == r){
        if (x[l] % 2 == 0) return x[l];
        return INT_MAX;  // nếu không chẵn thì trả về giá trị rất lớn
    }
    int m = (l + r) / 2;
    int min_left = min_even_value(x, l, m);
    int min_right = min_even_value(x, m+1, r);
    return min(min_left, min_right);
}

int main(){
    int a[] = {5, 7, 2, 9, 8, 11};
    int n = sizeof(a)/sizeof(a[0]);
    int result = min_even_value(a, 0, n-1);
    if (result == INT_MAX) cout << "Khong co so chan nao\n";
    else cout << "So chan nho nhat: " << result << endl;
}
So chan nho nhat: 2
Tìm giá trị chẵn lớn nhất trong mảng bằng chia để trị
#include <iostream>
#include <climits>
using namespace std;

int max_even_value(int x[], int l, int r){
    if (l == r){
        if (x[l] % 2 == 0) return x[l];
        return INT_MIN;  // nếu không chẵn thì trả về giá trị rất lớn
    }
    int m = (l + r) / 2;
    int min_left = max_even_value(x, l, m);
    int min_right = max_even_value(x, m+1, r);
    return max(min_left, min_right);
}

int main(){
    int a[] = {1, 2, 5, 7, 9, 8, 11};
    int n = sizeof(a)/sizeof(a[0]);
    int result = max_even_value(a, 0, n-1);
    if (result == INT_MIN) cout << "Khong co so chan nao\n";
    else cout << "So chan long nhat: " << result << endl;
}
Tính tổng các số dương trong mảng
#include <iostream>
using namespace std;

int sum(int x[], int l, int r) {
    if (l == r) {
        if (x[l] > 0) return x[l];
        else return 0;
    } else {
        int m = (l + r) / 2;
        int sum_left = sum(x, l, m);
        int sum_right = sum(x, m+1, r);
        return sum_left + sum_right;
    }
}

int main() {
    int a[] = {5, -2, 7, 0, -3, 4};
    int n = sizeof(a)/sizeof(a[0]);
    cout << "Tong cac so duong = " << sum(a, 0, n-1) << endl;
}
Tong cac so duong = 16   // (5 + 7 + 4)
Thuật toán pow(a, n)
Output = 243
int helper(int a, int n) {
	if (a == 0) return 0;
	if (n == 0) return 1;
	int res = helper(a * a, n / 2);
	if (n % 2 != 0) return a * res;
	else return res;
}

int power(int a, int n) {
	if (n > 0) return helper(a, n);
	else if (n == 0) return 1;
	else if (a == 0) return 0;
	else return 1.0 / helper(a, -1 * n);
}
cout << power(3,5);
Sắp xếp trộn
#include <bits/stdc++.h>
using namespace std;
void merge(int x[], int l, int m, int r){
    int n1 = m-l+1; // số phần tử nhánh trái
    int n2 = r-(m+1)+1; // số phần tử nhánh phải
    int L[n1], R[n2];
    for (int i = 0; i<n1; i++) L[i] = x[l+i]; // lất từ l -> m
    for (int j = 0; j<n2; j++) R[j] = x[m+1+j]; //lấy từ m+1 -> r
    int i = 0, j = 0, k = l;
    while(i<n1 && j<n2){
        if(L[i] <= R[j]) x[k++] = L[i++];
        else x[k++] = R[j++];
    }
    while (i < n1) x[k++] = L[i++];
    while (j < n2) x[k++] = R[j++];
}

void merge_sort(int x[], int l, int r){
    if (l < r){ // nếu mảng có nhiều hơn 1 phần tử thì đệ quy, 1 phần tử thì dừng
        int m = (l+r)/2;
        merge_sort(x, l, m);
        merge_sort(x, m+1, r);
        merge(x, l, m, r);
    }
}

int main(){
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Mang ban dau: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;

    merge_sort(arr, 0, n - 1); // gọi merge sort

    cout << "Mang sau khi sap xep: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    return 0;
}

Mang ban dau: 38 27 43 3 9 82 10 
Mang sau khi sap xep: 3 9 10 27 38 43 82
#include <bits/stdc++.h>
using namespace std;

void merge(vector<double> &x, int l, int m, int r){
	vector<double> left(x.begin() + l, x.begin()+m+1); //so phan tu nhanh trai
	vector<double> right(x.begin()+m+1, x.begin()+r+1); // so phan tu nhanh phai
	int i = 0; // index nhanh trai
	int j = 0; // index nhanh phai
	int k = l; // index nhanh chinh
	while (i < left.size() && j < right.size()){
		if (left[i] < right[j]) x[k++] = left[i++];
		else x[k++] = right[j++];
	}
	while (i < left.size()) x[k++] = left[i++];
	while (j < right.size()) x[k++] = right[j++];
}

void merge_sort(vector<double> &x, int l, int r){
	if (l < r){
		int m = (l+r)/2;
		merge_sort(x, l, m);
		merge_sort(x, m+1, r);
		merge(x, l, m, r);
	}
}

int main(){
	int min = 0;
	int max = 50;
	srand(time(0));
	
	vector<double> li;
	int n = 10;
	for (int i = 0; i < n; i++){
		double r = min + ((double)rand()/RAND_MAX)*(max-min);
		li.push_back(r);
	}
	for (int i = 0; i < n; i++){
		cout << li[i] << " ";
	}
	cout << endl;
	merge_sort(li, 0, li.size()-1);
	for (int i = 0; i < n; i++){
		cout << li[i] << " ";
	}
	return 0;
}