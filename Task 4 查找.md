

# Task 4 查找

#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

**暴力法**

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for(int i=0; i<nums.length; i++){
            for(int j=i+1; j<nums.length; j++){
                if (nums[i] + nums[j] == target){
                    return new int[] {i,j};
                }
            }
        }
    throw new IllegalArgumentException("No two sum solution");
    }
}
```

**一次哈希法**

将nums中的元素存储在一个哈希表中，key为元素的值，value为元素的索引。

存储之前首先判断目标和target 减去该元素的值是否已经存储在哈希表中，如果有，即为要寻找的元素对， 如果没有，则把该元素存储在哈希表中。

当遍历完整个nums时，仍没有返回元素对的索引，则抛出不存在的异常。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i< nums.length; i++){
            int complement = target - nums[i];
            if(map.containsKey(complement)){
                return new int[]{map.get(complement),i};
            }
            map.put(nums[i],i);
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```



#### [15. 三数之和](https://leetcode-cn.com/problems/3sum/)

将list先进行排序，然后寻找index i之后的两数和为0-nums[i] 的组合

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
            int target = 0-nums[i];
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



#### [18. 四数之和](https://leetcode-cn.com/problems/4sum/)

Leetcode上的题解，较三数之和的思路多了一重循环。

```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums,int target){
        List<List<Integer>> result=new ArrayList<>();
        if(nums==null||nums.length<4){
            return result;
        }
        Arrays.sort(nums);
        int length=nums.length;
        for(int k=0;k<length-3;k++){
            if(k>0&&nums[k]==nums[k-1]){
                continue;
            }
            int min1=nums[k]+nums[k+1]+nums[k+2]+nums[k+3];
            if(min1>target){
                break;
            }
 
            int max1=nums[k]+nums[length-1]+nums[length-2]+nums[length-3];
            if(max1<target){
                continue;
            }
           
            for(int i=k+1;i<length-2;i++){
                if(i>k+1&&nums[i]==nums[i-1]){
                    continue;
                }
                int j=i+1;
                int h=length-1;
                int min=nums[k]+nums[i]+nums[j]+nums[j+1];
                if(min>target){
                    break;
                }
                int max=nums[k]+nums[i]+nums[h]+nums[h-1];
                if(max<target){
                    continue;
                }
             
                while (j<h){
                    int curr=nums[k]+nums[i]+nums[j]+nums[h];
                    if(curr==target){
                        result.add(Arrays.asList(nums[k],nums[i],nums[j],nums[h]));
                        j++;
                        while(j<h&&nums[j]==nums[j-1]){
                            j++;
                        }
                        h--;
                        while(j<h&&i<h&&nums[h]==nums[h+1]){
                            h--;
                        }
                    }else if(curr>target){
                        h--;
                    }else {
                       j++;
                    }
                }
            }
        }
        return result;
    }
}
```



#### [219. 存在重复元素 II](https://leetcode-cn.com/problems/contains-duplicate-ii/)

滑动窗口法

```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        int len = nums.length;
        for (int i = 0; i<len; i++){
            for (int j = Math.max(i-k,0); j<i; j++){
                if(nums[i] == nums[j]){
                    return true;
                }
            }
        }
        return false;
    }
}
```

#### [220. 存在重复元素 III](https://leetcode-cn.com/problems/contains-duplicate-iii/)

滑动窗遍历搜索，超时

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        int len = nums.length;
        for (int i = 0; i<len; i++){
            for (int j = Math.max(i-k,0); j<i; j++){
                if(Math.abs(nums[i] - nums[j]) <= t){
                    return true;
                }
            }
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        TreeSet<Integer> set = new TreeSet<>();
        for (int i = 0; i < nums.length; i++) {
            Integer s = set.ceiling(nums[i]);
            if (s != null && s <= nums[i] + t) return true;
            Integer g = set.floor(nums[i]);
            if (g != null && nums[i] <= g + t) return true;
            set.add(nums[i]);
            if (set.size() > k) {
                set.remove(nums[i - k]);
            }
        }
        return false;
    }
}
```



#### [447. 回旋镖的数量](https://leetcode-cn.com/problems/number-of-boomerangs/)

```java
class Solution {
    public int numberOfBoomerangs(int[][] points) {
        int res = 0;
        for(int i = 0; i < points.length;i++){
            Map<Integer, Integer> record = new HashMap<>();
            for(int j = 0; j < points.length; j ++){
                if( j != i )
                    if(record.containsKey(distance(points[i], points[j]))){
                        record.put(distance(points[i], points[j]),
                                record.get(distance(points[i], points[j])) + 1);
                    }
                    else
                        record.put(distance(points[i], points[j]), 1);
            }
            for(int k : record.values()){
                    res += k * (k - 1);
            }
            
        }
        return res;
    }

    public int distance(int[] x, int[] y){
        return (x[0]-y[0])*(x[0]-y[0]) + (x[1]-y[1])*(x[1]-y[1]);
    }
}
```



#### [49. 字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        if (strs.length == 0) {
            return new ArrayList();
        }
        Map<String, List> ans = new HashMap<String, List>();
        for (String s : strs) {
            char[] chars = s.toCharArray();
            Arrays.sort(chars);
            String key = String.valueOf(chars);
            if (!ans.containsKey(key)) {
                ans.put(key, new ArrayList());
            }
            ans.get(key).add(s);
        }
        return new ArrayList(ans.values());

    }
}
```



#### [149. 直线上最多的点数](https://leetcode-cn.com/problems/max-points-on-a-line/)

```

```











