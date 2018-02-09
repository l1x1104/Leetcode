[预测赢家](https://leetcode.com/problems/predict-the-winner/description/)

- Solution 1: Recursion
```java
class Solution {
    public boolean PredictTheWinner(int[] nums) {
        return helper(nums, 0, nums.length - 1) >= 0;
    }
   
    private int helper(int[] nums, int start, int end) {
        if (start >= end) {
            return nums[end];
        }
        int left = helper(nums, start + 1, end);
        int right = helper(nums, start, end - 1);
        
        return Math.max(nums[start] - left, nums[end] - right);
    }
}
```

- Solution 2: DP
