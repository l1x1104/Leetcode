[输出比赛匹配对](https://leetcode.com/problems/output-contest-matches/description/)

```java
class Solution {
    public String findContestMatch(int n) {
        List<String> numbers = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            numbers.add(Integer.toString(i));
        }
        
        while (n > 1) {
            for (int i = 0; i < n / 2; i++) {
                String str = "(" + numbers.get(i) + "," + numbers.get(n - i - 1) + ")";
                numbers.set(i, str);
            }
            n /= 2;
        }
        
        return numbers.get(0);
    }
}
```
