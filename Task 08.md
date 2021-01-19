# Task 08

#### [78. 子集](https://leetcode-cn.com/problems/subsets/)

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        length = len(nums)
        
        def back(i, tmp):
            res.append(tmp)
            for j in range(i,length):
                back(j+1, tmp + [nums[j]])

        back(0,[])
        return res
```

#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

```java
class Solution {
    public int climbStairs(int n) {
        if (n == 1) return 1;
        int first = 1;
        int second = 2;
        for (int i = 3; i<=n; i++){
            int tem = first + second;
            first = second;
            second = tem;
            }
        return second;
    }
}
```

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1: 
            return 1
        first = 1
        second = 2
        for i in range(3,n+1):
            tem = first + second
            first = second
            second = tem
        return second
```

#### [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1 for i in range(n)]] + [[1] + [0 for i in range(n - 1)] for _ in range(m - 1)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return(dp[m - 1][n - 1])
```



