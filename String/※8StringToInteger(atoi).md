[字符串转为整数](https://leetcode.com/problems/string-to-integer-atoi/description/) <br>
这题难题是Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.
```java
class Solution {
    public int myAtoi(String str) {
        int n = str.length();
        if (n == 0) {
            return 0;
        }
        
        int i = 0, sign = 1, base = 0;
        char[] ch = str.toCharArray();
        while (i < n && ch[i] == ' ') {
            i++;
        }
        if (ch[i] == '+' || ch[i] == '-') {
            sign = (ch[i++] == '+') ? 1 : -1;
        }
        while (i < n && ch[i] >= '0' && ch[i] <= '9') {
            if (base > Integer.MAX_VALUE / 10 || (base == Integer.MAX_VALUE / 10 && ch[i] - '0' > 7)) {
                return (sign == 1) ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            }
            base = 10 * base + (ch[i++] - '0');
        }  
        
        return base * sign;
    }
}
```
