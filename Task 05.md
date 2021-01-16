# Task 05

23、26、33

#### [26. 删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        length = len(nums)
        i = 0
        for j in range(length):
            if nums[i] != nums[j]:
                i += 1
                nums[i] = nums[j]
        return i+1
```

#### [33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1
        l = 0
        r = len(nums) - 1
        while l<=r:
            m = (l+r) //2
            if nums[m] == target:
                return m
            if nums[0] <= nums[m]:
                if nums[0] <= target < nums[m]:
                    r = m - 1
                else:
                    l = m + 1
            else:
                if nums[m] < target <= nums[len(nums) - 1]:
                    l = m + 1
                else:
                    r = m - 1
        return -1
```

#### [23. 合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if not lists:
            return None
        import heapq
        tmp = []
        for l in lists:
            while l:
                tmp.append(l.val)
                l = l.next
        tmp.sort()
        res = ListNode(None)
        cur = res
        for i in tmp:
            temp_node = ListNode(i)
            cur.next = temp_node
            cur = temp_node
        return res.next
```

