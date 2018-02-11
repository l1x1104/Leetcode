[猜数字大小](https://leetcode.com/problems/guess-number-higher-or-lower-ii/description/)

```
For example,     [1,  2,  3,  4,  5,  6]
                  1  [2,  3,  4,  5]  6
                  k = 2,  3,  4,  5
                  j代表右区间，i代表左区间，k代表区间[i, j](不包括端点)内取任意一点的最小值.
```
```java
class Solution {
    public int getMoneyAmount(int n) {
        int[][] table = new int[n + 1][n + 1];
        for (int j = 2; j <= n; j++) {            
            for (int i = j - 1; i >= 1; i--) {
                int global_min = Integer.MAX_VALUE;
                for (int k = j - 1; k > i; k--) {
                    int local_max = k + Math.max(table[i][k - 1], table[k + 1][j]);
                    global_min = Math.min(local_max, global_min);
                }
                table[i][j] = i + 1 == j ? i : global_min;
            }
            
        }
        
        return table[1][n];
    }
}
```
