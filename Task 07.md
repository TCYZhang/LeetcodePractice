# Task 07

#### [61. 旋转链表](https://leetcode-cn.com/problems/rotate-list/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if not head:
            return None
        if head.next == None:
            return head
        
        tail = head
        length = 1
        while tail.next != None:
            tail = tail.next
            length += 1
        tail.next = head

        k = k % length

        for i in range(length-k):
            tail = tail.next
        new_head = tail.next
        tail.next = None
        return new_head
```

#### [54. 螺旋矩阵](https://leetcode-cn.com/problems/spiral-matrix/)

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        if not matrix or not matrix[0]:
            return res

        r = len(matrix)
        c = len(matrix[0])
        l = 0
        ri = c - 1
        t = 0
        b = r - 1
        while l <= ri and t <= b:
            for c in range(l, ri+1):
                res.append(matrix[t][c])
            for r in range(t+1, b+1):
                res.append(matrix[r][ri])
            if l < ri and t < b:
                for c in range(ri - 1, l, -1):
                    res.append(matrix[b][c])
                for r in range(b, t, -1):
                    res.append(matrix[r][l])
            l += 1
            ri -= 1
            t += 1
            b -= 1
        return res
```

#### [59. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

```python
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        l = 0
        r = n-1
        t = 0
        b = n-1
        matrix = [[0 for i in range(n)] for j in range(n)]
        
        num = 1
        target = n*n
        while num <= target:
            for column in range(l, r + 1):
                matrix[t][column] = num
                num += 1
            t += 1
            for row in range(t,b+1):
                matrix[row][r] = num
                num += 1
            r -= 1
            for column in range(r, l-1, -1):
                matrix[b][column] = num
                num += 1
            b -= 1
            for row in range(b, t-1, -1):
                matrix[row][l] = num
                num += 1
            l += 1
        return matrix
```

Note: 华为笔试题

