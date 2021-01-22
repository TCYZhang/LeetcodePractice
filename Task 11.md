# Task 11

#### [136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

先排序，在判断每一对是否相等

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        length = len(nums)
        nums.sort()
        if length == 1:
            return nums[0]
        for i in range(0, length-1, 2):
            if nums[i] != nums[i+1]:
                return nums[i]
            if i+2 == (length-1):
                return nums[-1]
            
```

力扣解法：按位相与

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        return reduce(lambda x, y: x ^ y, nums)
```

#### [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        visited = set()
        while head:
            if head in visited:
                return True
            else:
                visited.add(head)
                head = head.next
        return False
```

```python
class Solution:
    def hasCycle(self, head: ListNode) -> bool:
        if not head or not head.next:
            return False
        fast = head.next
        slow = head
        while slow != fast:
            if not fast or not fast.next:
                return False
            slow = slow.next
            fast = fast.next.next
        return True

```

#### [142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)

```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return None
        visited = set()
        while head:
            if head in visited:
                return head
            else:
                visited.add(head)
                head = head.next
        return None
```

```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        fast = head
        slow = head
        while True:
            if not fast or not fast.next:
                return None
            slow = slow.next
            fast = fast.next.next
            if fast == slow:
                break
        fast = head
        while fast != slow:
            fast = fast.next
            slow = slow.next 
        return fast
```

