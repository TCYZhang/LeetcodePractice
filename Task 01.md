# Task 01

## 2. 两数相加

```Python
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        head = tail = ListNode()
        carry = res = 0
        
        while l1 or l2 or carry:
            res = carry

            if l1:
                res = l1.val + res
                l1 = l1.next
            if l2:
                res = l2.val + res
                l2 = l2.next
            carry, res = divmod(res, 10)
            tail.next = ListNode(res)
            tail = tail.next
        return head.next
```



## 4. [寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        nums1.extend(nums2)
        nums1.sort()
        n = len(nums1)
        if n % 2 ==0:
            return (nums1[(n-1)>>1]+nums1[n>>1])/2.
        else:
            return nums1[(n-1)>>1]
```



## 5. 最长回文串

https://leetcode-cn.com/problems/longest-palindromic-substring/

```Java
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
                if(chars[i] == chars[j]){
                //     dp[i][j] = false;
                // }else{
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

