# Task 10

121、122、124

#### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        for i in range(len(prices)):
            for j in range(i+1,len(prices)):
                res = max(res,prices[j]-prices[i])
        return res
```

暴力法，超时

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        res = 0
        minprice = prices[0]
        for i in range(1,len(prices)):
            res = max(res, prices[i]-minprice)
            minprice = min(minprice,prices[i])
        return res
```

在遍历价格数组时，记录当前遍历过的价格的最低价格和最大利润，每访问一个新的价格，都记录所能获得的最大利润值。

#### [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        length = len(prices)
        min = prices[0]
        res = 0
        for i in range(length):
            if(prices[i]<min):
                min = prices[i]
            elif(prices[i] > min):
                res += prices[i] - min;
                min = prices[i]
        return res
```

#### [124. 二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

leetcode 官方参考

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def __init__(self):
        self.maxSum = float("-inf")
    def maxPathSum(self, root: TreeNode) -> int:
        def maxGain(node):
            if not node:
                return 0
            leftGain = max(maxGain(node.left), 0)
            rightGain = max(maxGain(node.right), 0)
            priceNewpath = node.val + leftGain + rightGain
            self.maxSum = max(self.maxSum, priceNewpath)
            return node.val + max(leftGain, rightGain)
        maxGain(root)
        return self.maxSum
```



