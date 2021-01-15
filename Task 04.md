# Task 04

#### [16. 最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length;
        int diff = Math.abs(nums[0] + nums[1] + nums[2] - target);
        int res = nums[0] + nums[1] + nums[2];
        for(int i = 0; i<n; i++){
            int l = i+1;
            int r = n-1;
            int tem = target - nums[i];
            while(l<r){
                if (nums[l] + nums[r] == tem){
                    return  target;
                }else {
                    if(Math.abs(nums[l]+ nums[r] - tem)< diff){
                        diff = Math.abs(nums[l]+ nums[r] - tem);
                        res = nums[l]+ nums[r] + nums[i];
                    }
                    if (nums[l] + nums[r] < tem){
                        l++;
                    }else{
                        r--;
                    }
                }
            }
        }
        return res;
    }
}
```



#### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 == 1:
            return False
        else:
            pairs = {
            ")": "(",
            "]": "[",
            "}": "{",
            }
        stack = []
        for ch in s:
            if ch in pairs:
                if len(stack) or stack[-1] != pairs[ch]:
                    return False
                stack.pop()
            else:
                stack.append(ch)
        return not stack
```

#### [21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

```python
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        if l2 is None :
            return l1
        elif l1 is None:
            return l2
        elif l1.val <= l2.val:
            l1.next = self.mergeTwoLists(l1.next,l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2 
```

