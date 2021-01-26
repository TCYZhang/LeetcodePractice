# Task 14

#### [217. 存在重复元素](https://leetcode-cn.com/problems/contains-duplicate/)

用set 存储已经访问过的元素，遍历数组的同时判断元素是否已经存储在visited中

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        visited = set()
        for item in nums:
            if item in visited:
                return True
            else:
                visited.add(item)
        return False        
```

#### [230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        def inorder(r):
            if not r:
                return []
            left = inorder(r.left) if r.left else []
            right = inorder(r.right) if r.right else []
            return left + [r.val] + right
        
        return inorder(root)[k-1]
```

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        tmp = []
        while 1 :
            while root:
                tmp.append(root)
                root = root.left
            root = tmp.pop()
            k -= 1
            if k == 0:
                return root.val
            else:
                root = root.right
```

#### [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        def swap(nums, i, j):
            tmp = nums[i]
            nums[i] = nums[j]
            nums[j] = tmp

        def heapify(nums,length):
            n = length // 2
            for i in range(n, 0, -1):
                bubbleDown(i, nums, n)
        
        def bubbleDown(i, nums, n):
            left = 2*i + 1
            right = 2*i + 2
            if left > n:
                return
            elif right > n:
                if nums[i] < nums[left]:
                    swap(nums, i, left)
            else:
                if nums[left] > nums[right]:
                    if nums[i] < nums[left]:
                        swap(nums, i, left)
                        bubbleDown(left, nums, n)
                else:
                    if nums[i] < nums[right]:
                        swap(nums, i, right)
                        bubbleDown(right, nums, n)
        
        # def deleteMax():
        #     maxNumber = nums[0]
        #     nums[0] = nums[length-1]
        #     bubbleDown(0, nums, length)
        #     return maxNumber 

        length = len(nums)
        n = length
        heapify(nums,length)
        for i in range(n-1, n-k+1, -1):
            swap(nums, 0, length)
            length -= 1
            bubbleDown(0, nums, length)
        return nums[0]
```

*Note: the program needs more check!*

