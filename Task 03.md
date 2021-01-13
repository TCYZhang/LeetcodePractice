# Task 03

#### [11. 盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

双指针法

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        maxarea = 0
        l = 0
        r = len(height) - 1
        while l < r:
            maxarea = max(maxarea, min(height[l],height[r])*(r-l))
            if height[l]<height[r]:
                l += 1
            else:
                r -= 1
        return maxarea
```

#### [14. 最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0:
            return ""
        strs.sort()
        length, count = len(strs[0]), len(strs)
        for i in range(length):
            c = strs[0][i]
            if any(i == len(strs[j]) or strs[j][i] != c for j in range(1, count)):
                return strs[0][:i]
              
        return strs[0]
```

#### [15. 三数之和](https://leetcode-cn.com/problems/3sum/)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        List<List<Integer>> ans = new ArrayList<List<Integer>>();
        for (int i = 0; i < n-2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            int r = n - 1;
            int target = -nums[i];
            for (int l = i + 1; l < n; l++) {
                if (l > i + 1 && nums[l] == nums[l - 1]) {
                    continue;
                }
                while (l < r && nums[l] + nums[r] > target) {
                    r--;
                }
                if (l == r) {
                    break;
                }
                if (nums[l] + nums[r] == target) {
                    List<Integer> list = new ArrayList<Integer>();
                    list.add(nums[i]);
                    list.add(nums[l]);
                    list.add(nums[r]);
                    ans.add(list);
                }
            }
        }
        return ans;
    }
}
```



