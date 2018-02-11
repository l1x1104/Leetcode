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
```java
class Solution {
    public boolean PredictTheWinner(int[] nums) {
        int n = nums.length;
        if (nums == null || n == 0) {
            return true;
        }
        
        int[][] table = new int[n][n];
        for (int i = 0; i < n; i++) {
            table[i][i] = nums[i];
        }
        
        for (int i = 1; i < n; i++) {
            for (int j = 0, k = i; k < n; j++, k++) {
                table[j][k] = Math.max(nums[j] - table[j + 1][k], nums[k] - table[j][k - 1]);
            }
        }
        
        return table[0][n - 1] >= 0;
    }  
}
```
