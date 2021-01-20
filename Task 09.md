#  Task 09

#### [88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        p1 = m-1
        p2 = n-1
        p = m + n -1

        while p1>=0 and p2>=0:
            if nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1
            p -= 1
        nums1[:p2 + 1] = nums2[:p2 + 1]
```

#### [104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null){
            return 0;
        }
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        return Math.max(left,right) + 1;
    }
}
```

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        left = self.maxDepth(root.left)
        right = self.maxDepth(root.right)
        return max(left,right) + 1
```

#### [89. 格雷编码](https://leetcode-cn.com/problems/gray-code/)

```python
class Solution:
    def grayCode(self, n: int) -> List[int]:
   
        res = [0]
        head = 1
        for i in range(n):
            for j in range(head - 1, -1, -1):
                res.append(head+res[j])
            head = head << 1
        return res
```

