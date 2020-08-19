# Task 1 分治

分治，分而治之 MapReduce

#### [50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

![image-20200819121308364](/Users/cyzhang/Desktop/Datawhale leetcode/image-20200819121308364.png)

当n为正数时，用上面ppt里面递归的思路很简单。

但是在这个题目的测试用例中存在负数的情况，需要考虑正负数的转换。

```java
class Solution {
    public double myPow(double x, int n) {
        long N = n;
        if (N >=0){
            return helper(x, N);
        }else{
            return 1.0/helper(x, -N);
        }
        
    }

    public double helper(double x, long n){
        double res = 1.0;
        if(n == 0){
            return res;
        }
        while(n>0){
            if(n%2 == 1){
                res *= x;
            }
            x = x*x;
            n /= 2;
        }
        return res;
    }
}
```



#### [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

**贪心法**

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = 0;
        int result = nums[0];
        for(int number : nums){
            if(sum > 0){
                sum += number;
            }else{
                sum = number;
            }
            result = Math.max(sum, result);
        }
        return result;
    }
}
```

**分治法**

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



#### [169. 多数元素](https://leetcode-cn.com/problems/majority-element/)

```java
class Solution {
    public int majorityElement(int[] nums) {
        return helper(nums, 0, nums.length-1);
    }

    public int count(int[] nums, int num, int left, int right){
        int count = 0;
        for (int i = left; i<=right; i++){
            if (nums[i] == num) count ++;
        }
        return count;
    }

    public int helper(int[] nums, int left, int right){
        if(left == right){
            return nums[left];
        }

        int mid = (left + right)/2;
        int le = helper(nums, left, mid);
        int ri = helper(nums, mid+1, right);

        int leftCount = count(nums, le, left, right);
        int rightCount = count(nums, ri, left, right);

        return leftCount > rightCount ? le : ri;

    }
}
```

