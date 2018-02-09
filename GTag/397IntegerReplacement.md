[整数替换]（https://leetcode.com/problems/integer-replacement/description/）

```java
class Solution {
    private int result = Integer.MAX_VALUE;
    public int integerReplacement(int n) {
        if (n == Integer.MAX_VALUE) {
            return 32;
        }
        helper(n, 0);
        return result;
    }
    private void helper(int n, int len) {
        if (n < 1) {
            return ;
        }
        if (n == 1) {
            result = Math.min(len, result);
            return ;
        }
        if (n % 2 == 0) {
            helper(n / 2, len + 1);
        } else {
            helper(n - 1, len + 1);
            helper(n + 1, len + 1);
        }
    }
}
```
