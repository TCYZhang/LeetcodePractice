# Task 06

43、46、53

#### [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        int size = nums.length;
        res = helper(nums, 0, size - 1);
        return res;
    }

    public int helper(int[] nums, int left, int right){
        if(left == right){
            return nums[left];
        }
        int mid = (left + right) /2;
        int leftSum = helper(nums, left, mid);
        int rightSum = helper(nums, mid + 1, right);
        int midSum = cross(nums, left, mid, right);
        int result = Math.max(leftSum, rightSum);
        result = Math.max(result, midSum);
        return result;
    }

    public int cross(int[] nums, int left,int mid, int right){
        int leftSum = nums[mid];
        int sum = 0;
        for (int i = mid; i >= left; i--)
        {
            sum += nums[i];
            leftSum = Math.max(leftSum, sum);
        }

        int rightSum = nums[mid+1];
        sum = 0;
        for (int i = mid + 1; i <= right; i++)
        {
            sum += nums[i];
            rightSum = Math.max(rightSum, sum);
        }
        return (leftSum + rightSum);

    }
}
```

#### [43. 字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        if num1 == '0' or num2 == '0':
            return '0'
        m = len(num1)
        n = len(num2)
        resArr = [0 for i in range(m+n)]

        for i in range(m-1, -1, -1):
            x = int(num1[i])
            for j in range(n-1, -1, -1):
                resArr[i+j+1] += x * int(num2[j])

        for i in range(m+n-1, 0, -1):
            resArr[i-1] += resArr[i] // 10
            resArr[i] = resArr[i] % 10

        s = 1 if resArr[0] == 0 else 0
        res = "".join(str(x) for x in resArr[s:])
        return res
```

#### [46. 全排列](https://leetcode-cn.com/problems/permutations/)

```python
class Solution:
    def dfs(self,nums, length, depth, path, used, res):
        if length == depth:
            res.append([item for item in path])
            return
        
        for i in range(length):
            if used[i]:
                continue
            path.append(nums[i])
            used[i] = True
            self.dfs(nums, length, depth+1, path, used, res)
            path.remove(nums[i])
            used[i] = False

    def permute(self, nums: List[int]) -> List[List[int]]:
        length = len(nums)
        res = []
        depth = 0
        if length == 0:
            return res
        
        path = []
        used = [False for i in range(length)]
        self.dfs(nums, length, depth, path, used, res)
        return res
```



