[两个字符串的删除操作](https://leetcode.com/problems/delete-operation-for-two-strings/description/)

```java
class Solution {
    public int minDistance(String A, String B) {
        int n = A.length();
        int m = B.length();
        int f[][] = new int[n + 1][m + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                f[i][j] = Math.max(f[i - 1][j], f[i][j - 1]);
                if(A.charAt(i - 1) == B.charAt(j - 1))
                    f[i][j] = f[i - 1][j - 1] + 1;
            }
        }
        int val = f[n][m];
        return (n - val) + (m - val);
    }
}
```
