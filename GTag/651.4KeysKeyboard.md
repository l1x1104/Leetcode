[四键的键盘](https://leetcode.com/problems/4-keys-keyboard/description/)

- Solution 1: Recursion
```java
class Solution {
    public int maxA(int N) {
        int res = N;
        for (int i = 1; i < N - 2; ++i) {
            res = Math.max(res, maxA(i) * (N - 1 - i));
        }
        return res;
    }
}
```

- Solution 2: DP
```java
class Solution {
    public int maxA(int N) {
        if (N <= 6)  return N;
        
        int[] dp = new int[N + 1];
        for (int i = 1; i <= 6; i++) {
            dp[i] = i;
        }
        
        for (int i = 7; i <= N; i++) {
            dp[i] = Math.max(dp[i - 4] * 3, dp[i - 5] * 4); 
        }
        
        return dp[N];
  }
}
```
