# Task 13

#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# class Solution:
#     def reverseList(self, head: ListNode) -> ListNode:
#         res = None
#         while head != None:
#             tmp = head.next 
#             head.next = res
#             res = head
#             head = tmp
#         return res

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        res = None
        current = head
        while current != None:
            tmp = current.next 
            current.next = res
            res = current
            current = tmp
        return res
```

#### [169. 多数元素](https://leetcode-cn.com/problems/majority-element/)

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        index = len(nums) // 2
        return nums[index]
```

#### [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        pA = headA
        pB = headB
        while pA != pB:
            if pA:
                pA = pA.next
            else:
                pA = headB
            if pB:
                pB = pB.next
            else:
                pB = headA
        return pA
```

