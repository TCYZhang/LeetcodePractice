# Task3 查找

#### [35. 搜索插入位置](https://leetcode-cn.com/problems/search-insert-position/)

**二分查找**

- 设置左右下标 left、right 和中间下标 mid
- 根据 nums[mid] 和 target 的值大小关系进行操作的判断
  - nums[mid] == target  返回mid
  - nums[mid] > target  right 左移
  - nums[mid] < target  left 右移
- 查找结束没有target时，则返回left， 这个值为最后插入的位置。

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int length = nums.length;
        int left = 0;
        int right = length -1;
        int res = length;
        while(left <= right){
            int mid = left + (right - left)/2;
            if(target <= nums[mid]){
                res = mid;
                right = mid - 1;
            }else{
                left = mid + 1;
            }
        }
        return res;
    }
}
```

```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        left = 0
        right = len(nums)-1
        res = len(nums)
        while left <= right:
            mid = (left + right)//2
            if nums[mid] >= target:
                res = mid
                right = mid - 1
            else:
                left = mid + 1
        return res
```



#### [202. 快乐数](https://leetcode-cn.com/problems/happy-number/)

用set存储已经出现的结果

```java
class Solution {
    public int helper(int n){
        int sum = 0;
        int tmp = 0;
        while(n > 0){
            tmp = n % 10;
            sum += tmp*tmp;
            n = n/10;
        }
        return sum;
    }

    public boolean isHappy(int n) {
        Set<Integer> exist = new HashSet<>();
        exist.add(n);
        while(n != 1){
            n = helper(n);
            if(!exist.add(n)){
                return false;
            }
        }
        return true;
    }
}
```

**快慢指针法**：

```java
class Solution {
    public int helper(int n){
        int sum = 0;
        int tmp = 0;
        while(n > 0){
            tmp = n % 10;
            sum += tmp*tmp;
            n = n/10;
        }
        return sum;
    }

    public boolean isHappy(int n) {
        int slow = n;
        int fast = n;
        do{
            slow = helper(slow);
            fast = helper(helper(fast));
        }while(slow != fast);
        return (slow == 1);
    }
}
```



#### [290. 单词规律](https://leetcode-cn.com/problems/word-pattern/)

通过map 构造pattern和str 的出现顺序，判断两者的模式是否相同。

```java
class Solution {
    public boolean wordPattern(String pattern, String str) {
        String[] words = str.split(" ");
        if (pattern.length() != words.length){
            return false;
        }
        // String p = helper(pattern.split(""));
        // String w = helper(words);
        // return p.equals(w);
        return helper(pattern.split("")).equals(helper(words));
    }

    public String helper(String[] words){
        HashMap<String, Integer> map = new HashMap<>(); 
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < words.length; i++) {
            if (map.containsKey(words[i])) {
                sb.append(map.get(words[i]));
            } else {
                sb.append(i);
                map.put(words[i], i); 
            }
        }
        return sb.toString();

    }
}
```



#### [205. 同构字符串](https://leetcode-cn.com/problems/isomorphic-strings/)

与上一题的思路相同。

```java
class Solution {
    public boolean isIsomorphic(String s, String t) {
        // if(s.length() != t.length()){
        //     return false;
        // }
        return helper(s.split("")).equals(helper(t.split("")));
    }

    public String helper(String[] words){
        HashMap<String, Integer> map = new HashMap<>(); 
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < words.length; i++) {
            if (map.containsKey(words[i])) {
                sb.append(map.get(words[i]));
            } else {
                sb.append(i);
                map.put(words[i], i); 
            }
        }
        return sb.toString();
    }
}
```



#### [242. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)

将字符串中的字母存储在数组中，在进行排序，判断两个数组是否相等，从而判断是否为字母异位词。

```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()){
            return false;
        }
        char[] a = s.toCharArray();
        char[] b = t.toCharArray();
        Arrays.sort(a);
        Arrays.sort(b);

        return Arrays.equals(a,b);
    }
}
```





#### [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

```python
class Solution:
    def helper(self,nums1,nums2):
        return [x for x in nums1 if x in nums2]

    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        s1 = set(nums1)
        s2 = set(nums2)

        return self.helper(s1, s2)
```



#### [350. 两个数组的交集 II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)

将两个数组首先进行排序，然后逐一进行比较，当相等时，添加进result，并同时将index向后移。

```python
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        nums1.sort()
        nums2.sort()

        l1 = len(nums1)
        l2 = len(nums2)

        index1 = 0
        index2 = 0

        res = []

        while index1 < l1 and index2 < l2:
            if nums1[index1] == nums2[index2]:
                res.append(nums1[index1])
                index1 = index1 + 1
                index2 = index2 + 1
            elif nums1[index1] > nums2[index2]:
                index2 = index2 + 1
            elif nums1[index1] < nums2[index2]:
                index1 = index1 + 1

        return  res
```



#### [410. 分割数组的最大值](https://leetcode-cn.com/problems/split-array-largest-sum/)

Leetcode 参考代码

```python
class Solution:
    def splitArray(self, nums: List[int], m: int) -> int:
        def check(x: int) -> bool:
            total, cnt = 0, 1
            for num in nums:
                if total + num > x:
                    cnt += 1
                    total = num
                else:
                    total += num
            return cnt <= m


        left = max(nums)
        right = sum(nums)
        while left < right:
            mid = (left + right) // 2
            if check(mid):
                right = mid
            else:
                left = mid + 1

        return left

```









#### [451. 根据字符出现频率排序](https://leetcode-cn.com/problems/sort-characters-by-frequency/)

利用collection 库中counter函数：

```python
class Solution:
    def frequencySort(self, s: str) -> str:
        count = collections.Counter(s)
        res = ''
        for i, j in count.most_common():
            res += i*j
        return res
```

```python
class Solution:
    def frequencySort(self, s: str) -> str:
        return ''.join([i * j for i, j in collections.Counter(s).most_common()])
```







#### [540. 有序数组中的单一元素](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/)

暴力法：从头开始每两个元素遍历。

```python
class Solution:
    def singleNonDuplicate(self, nums: List[int]) -> int:
        for i in range(0, len(nums)-2, 2):
            if nums[i] != nums[i+1]:
                return nums[i]
        return nums[-1]
```

二分法： 判断中间位置与左边相等还是右边相等，同时根据左右的奇偶个数判断左右索引的变化。

```python
class Solution:
    def singleNonDuplicate(self, nums: List[int]) -> int:
        left = 0
        right = len(nums)-1
        while left < right:
            mid = left + (right - left)//2
            even = (right - mid)%2 == 0
            if nums[mid] == nums[mid+1]:
                if even:
                    left = mid + 2
                else: 
                    right = mid - 1
            elif nums[mid-1] == nums[mid]:
                if even:
                    right = mid - 2
                else:
                    left = mid + 1
            else:
                return nums[mid]
        return nums[left]
```

