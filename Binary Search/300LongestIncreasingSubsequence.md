[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/description/)

其中 dp[i] 表示以 nums[i] 为结尾的最长递增子串的长度，对于每一个 nums[i]，我们从第一个数再搜索到 i，如果发现某个数小于 nums[i]，我们更新 dp[i]，更新方法为 dp[i] = max(dp[i], dp[j] + 1)，即比较当前 dp[i] 的值和那个小于 num[i] 的数的 dp 值加 1 的大小，我们就这样不断的更新 dp 数组，到最后 dp 数组中最大的值就是我们要返回的 LIS 的长度
- Solution 1: DP O(n^2)
```java
class Solution {
    public int lengthOfLIS(int[] nums) {        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        int[] dp = new int[nums.length];
        int result = 0;
        Arrays.fill(dp, 1);
        
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            result = Math.max(result,dp[i]);
        }
        
        return result;
    }
}
```

- Solution 2: Binary Search O(nlogn) <br>
Leetcode discussion <br>
```java
class Solution {
    public int lengthOfLIS(int[] nums) {        
        if (nums == null || nums.length == 0) {
            return 0;
        }
        
        List<Integer> tails = new LinkedList<>();
        tails.add(nums[0]);
        
        for (Integer num: nums) {
            if (num < tails.get(0)) {
                tails.set(0, num);
            } else if (num > tails.get(tails.size() - 1)) {
                tails.add(num);
            } else {
                int left = 0, right = tails.size() - 1;
                while (left < right) {
                    int mid = left + (right - left) / 2;
                    if (tails.get(mid) < num) {
                        left = mid + 1;
                    } else {
                        right = mid;
                    }
                }
                tails.set(left, num);
            }
        }
        
        return tails.size();
    }
}
```

