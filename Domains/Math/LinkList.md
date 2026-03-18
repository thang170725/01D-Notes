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