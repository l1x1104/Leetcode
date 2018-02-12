[输出比赛匹配对](https://leetcode.com/problems/output-contest-matches/description/)

```java
class Solution {
    public String findContestMatch(int n) {
        String[] result = new String[n];
        for (int i = 0; i < n; i++) {
            result[i] = Integer.toString(i + 1);
        }
        
        while (n > 1) {
            for (int i = 0; i < n / 2; i++) {
                result[i] = "(" + result[i] + "," + result[n - i - 1] + ")";
            }
            n /= 2;
        }
        
        return result[0];
    }
}
```
