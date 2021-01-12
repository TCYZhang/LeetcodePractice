# Task 01

## [7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)

```python
class Solution:
    def reverse(self, x: int) -> int:
        res = 0
        while x != 0:
            if ((res * 10) / 10) != res:
                res = 0
                break
            res = res * 10 + x % 10
            x = x / 10
        return res
```

```Java
class Solution {
    public int reverse(int x) {
	int ans = 0;
	while (x != 0) {
		if ((ans * 10) / 10 != ans) {
			ans = 0;
			break;
		}
		ans = ans * 10 + x % 10;
		x = x / 10;
	}
	return ans;
}
}
```



#### [8. 字符串转换整数 (atoi)](https://leetcode-cn.com/problems/string-to-integer-atoi/)

力扣题解：正则表达式

```python
class Solution:
    def myAtoi(self, s: str) -> int:
        return max(min(int(*re.findall('^[\+\-]?\d+', s.lstrip())), 2**31 - 1), -2**31)
```



#### [9. 回文数](https://leetcode-cn.com/problems/palindrome-number/) 

```python
class Solution:
    def isPalindrome(self, x: int) -> bool:
        if x<0 or (x%10 == 0 and x!= 0):
            return False

        revertedNumber = 0
        while x > revertedNumber:
            revertedNumber = revertedNumber * 10 + x % 10
            x = x//10

        return x == revertedNumber or x == revertedNumber // 10
```

