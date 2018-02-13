[炸弹人](https://leetcode.com/problems/bomb-enemy/description/)

```java
class Solution {
    public int maxKilledEnemies(char[][] grid) {
        if (grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int m = grid.length, n = grid[0].length, res = 0, rowCnt = 0;
        int[] colCnt = new int[n];
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (j == 0 || grid[i][j - 1] == 'W') {
                    rowCnt = 0;
                    for (int k = i; k < n && grid[i][k] != 'W'; ++k) {
                        rowCnt += grid[i][k] == 'E' ? 1 : 0;
                    }
                }
                
                if (i == 0 || grid[i - 1][j] == 'W') {
                    colCnt[j] = 0;
                    for (int k = j; k < m && grid[k][j] != 'W'; ++k) {
                        colCnt[j] += grid[k][j] == 'E' ? 1 : 0;
                    }
                }
                
                if (grid[i][j] == '0') {
                    res = Math.max(res, rowCnt + colCnt[j]);
                }
            }
        }
        
        return res;
    }
}
```
