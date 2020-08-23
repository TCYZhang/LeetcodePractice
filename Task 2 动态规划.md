# Task 2 动态规划

#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

**递归**

时间复杂度较高，在Leetcode上会超时。

```java
class Solution {
    public int climbStairs(int n) {
        if(n == 1){
            return 1;
        }
        if(n ==)2{
          return 2;
        }else{
          return climbStairs(n-1) + climbStairs(n-2);
        }
    }
}
```



**动态规划**

```java
class Solution {
    public int climbStairs(int n) {
        if(n == 1){
            return 1;
        }
        int[] dp = new int[n+1];
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```



**斐波那契数列**

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

Java 的运行速度比python快， 但是内存的消耗比python高。





#### [300. 最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

dp 为一个长度和nums相同的数组，数组的第i个元素对应着到i为止的最长上升子序列；

对于nums中的每一个元素，判断它与前面每一个元素的大小关系，并判断dp数组中应存储的最长子序列数。

```Java
class Solution {
    public int lengthOfLIS(int[] nums) {
        int len = nums.length;
        if(len == 0){
            return 0;
        }
        int[] dp = new int[len];
        dp[0] = 1;
        int result = 1;
        for (int i = 1; i<dp.length; i++){
            int value = 0;
            for (int j= 0; j<i; j++){
                if(nums[i] > nums[j]){
                    value = Math.max(value, dp[j]);
                }
            }
            dp[i] = value+1;
            result = Math.max(result, dp[i]);
        }
        return result;
    }
}
```

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        dp = [1]*len(nums)
        for i in range(len(nums)):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i],dp[j]+1)
        return max(dp)
```



#### [674. 最长连续递增序列](https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/)

dp为一个和nums长度相同的数组，数组中的每一个元素对应着相应的最长 **连续**递增的子序列；

对于dp中的每一个元素，其变化仅与nums中它前面的元素相关，所以进判断一次就可以得到最终的结果。 

```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int len = nums.length;
        if(len == 0){
            return 0;
        }
        int[] dp = new int[len];
        dp[0] = 1;
        int result = 1;
        for(int i = 1; i<len; i++){
            if (nums[i]>nums[i-1]){
                dp[i] = dp[i-1]+1;
                result = Math.max(result, dp[i]);
            }else{
                dp[i] = 1;
            }
        }
        return result;
    }
}
```

```python 
class Solution:
    def findLengthOfLCIS(self, nums: List[int]) -> int:
        if not nums: return 0
        dp = [1]*len(nums)
        for i in range(1, len(nums)):
            if nums[i]>nums[i-1]:
                dp[i]= dp[i-1]+1
        return max(dp)
```





#### [5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

**动态规划法**

```java
class Solution {
    public String longestPalindrome(String s) {
        int len = s.length();
        if (len<2){
            return s;
        }

        int maxLength = 1;
        int begin = 0;

        // Initialize the dp array.
        boolean[][] dp = new boolean[len][len];
        // The diagonal elements will not be used during the table filling procedure.
        // for(int i = 0; i<len; i++){
        //     dp[i][i] = true;
        // }

        char[] chars = s.toCharArray();

        // Filling the table column by column.
        for(int j = 1; j<len; j++){
            for(int i = 0; i<j; i++){
              //// The dp is initialized with false for boolean variables.
                //if(chars[i] != chars[j]){
                  //  dp[i][j] = false;
                //}else{
              if(chars[i] == chars[j]){
                    // Be careful with the boundary cases.
                    // Boundary conditions: j-1-(i+1)+1<2  ->   j-i<3
                    if(j-i<3){
                        dp[i][j] = true;
                    }else{
                        dp[i][j] = dp[i+1][j-1];
                    }
                }
                // Keep record of the begining position and length.
                if(dp[i][j] && j-i+1>maxLength){
                    maxLength = j-i+1;
                    begin = i;
                }
            }
        }
        return s.substring(begin, begin+maxLength);
    }
}
```

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        length = len(s)
        if length < 2:
            return s
        
        dp = [[False for _ in range(length)] for _ in range(length)]

        max_length = 1
        begin = 0

        for j in range(1,length):
            for i in range(j):
                if s[i] == s[j]:
                    if j-i<3:
                        dp[i][j] = True
                    else:
                        dp[i][j] = dp[i+1][j-1]
                if dp[i][j] and j-i+1 > max_length:
                    max_length = j-i+1
                    begin = i

        return s[begin:begin+max_length]
```



#### [516. 最长回文子序列](https://leetcode-cn.com/problems/longest-palindromic-subsequence/)

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int len = s.length();
        int[][] dp = new int[len][len];

        for(int i =0; i<len; i++){
            dp[i][i] =1;
        }

        char[] chars = s.toCharArray();

        for (int i = len-1; i>=0; i--){
            for(int j= i+1; j<len; j++){
                if(chars[i] == chars[j]){
                    dp[i][j] = dp[i+1][j-1]+2;
                }else{
                    dp[i][j] = Math.max(dp[i+1][j],dp[i][j-1]);
                }
            }
        }

        return dp[0][len-1];

    }
}
```

```python 
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        length = len(s)
        dp=[[0 for _ in range(length)] for _ in range(length)]
        for i in range(length):
            dp[i][i] = 1

        for i in range(length,-1,-1):
            for j in range(i+1,length):
                if s[i]==s[j]:
                    dp[i][j] = dp[i+1][j-1]+2
                else:
                    dp[i][j] = max(dp[i][j-1],dp[i+1][j])
        return dp[0][length-1]
```



#### [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

```java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if(len == 0){
            return 0;
        }
        if(len == 1){
            return nums[0];
        }
        int[] dp = new int[len];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i<len; i++){
            dp[i] = Math.max(dp[i-2]+nums[i], dp[i-1]);
        }
        return dp[len-1];
    }
}
```

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        length = len(nums)
        if length == 0:
            return 0
        if length == 1:
            return nums[0]
        dp = [0]*length
        dp[0] = nums[0]
        dp[1] = max(nums[0],nums[1])
        for i in range(2,length):
            dp[i] = max(dp[i-2]+nums[i],dp[i-1])
        return dp[-1]
```



#### [213. 打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

```java
class Solution {
    public int rob(int[] nums) {
        int len = nums.length;
        if(len == 0){
            return 0;
        }
        if(len == 1){
            return nums[0];
        }
        return Math.max(helper(Arrays.copyOfRange(nums, 0, len-1)),
        helper(Arrays.copyOfRange(nums, 1, len)));
        

    }

    public int helper(int[] nums) {
        int len = nums.length;
        if(len == 0){
            return 0;
        }
        if(len == 1){
            return nums[0];
        }
        int[] dp = new int[len];
        dp[0] = nums[0];
        dp[1] = Math.max(nums[0], nums[1]);
        for (int i = 2; i<len; i++){
            dp[i] = Math.max(dp[i-2]+nums[i], dp[i-1]);
        }
        return dp[len-1];
    }
}
```

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        def helper(nums):
            length = len(nums)
            if length == 0:
                return 0
            if length == 1:
                return nums[0]
            dp = [0]*length
            dp[0] = nums[0]
            dp[1] = max(nums[0],nums[1])
            for i in range(2,length):
                dp[i] = max(dp[i-2]+nums[i],dp[i-1])
            return dp[-1]
        
        length = len(nums)
        if length == 0:
            return 0
        if length == 1:
            return nums[0]
        return max(helper(nums[1:]), helper(nums[:-1]))
```



#### [72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)

```java
class Solution {
    public int minDistance(String word1, String word2) {
        int len1 = word1.length();
        int len2 = word2.length();

        if (len1 == 0 || len2 == 0){
            return len1+len2;
        }

        int[][] dp = new int[len1+1][len2+1];

        for(int i = 0; i<= len1; i++){
            dp[i][0] = i;
        }

        for (int j = 0; j<=len2; j++){
            dp[0][j] = j;
        }
        char[] chars1 = word1.toCharArray();
        char[] chars2 = word2.toCharArray();

        for (int i = 1; i<= len1; i++){
            for (int j = 1; j<= len2; j++){
                if(chars1[i-1] == chars2[j-1]){
                    dp[i][j] = dp[i-1][j-1];
                }else{
                    dp[i][j] = 1 + Math.min(dp[i-1][j-1], Math.min(dp[i][j-1],dp[i-1][j]));
                }
            }
        }
        return dp[len1][len2];
    }
}
```

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        length1 = len(word1)
        length2 = len(word2)

        if length1 ==0 or length2 == 0:
            return length1 + length2
        
        dp = [[0 for _ in range(length2+1)] for _ in range(length1+1)]

        for i in range(length1+1):
            dp[i][0] = i
        for j in range(length2+1):
            dp[0][j] = j
        
        for i in range(1,length1+1):
            for j in range(1,length2+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = 1 + min(dp[i-1][j-1],dp[i][j-1], dp[i-1][j])
        
        return dp[-1][-1]
```













