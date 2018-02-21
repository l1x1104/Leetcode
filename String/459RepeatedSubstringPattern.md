[Repeated Substring Pattern](https://leetcode.com/problems/repeated-substring-pattern/description/) <br>

Thinking path: 1. What is the substring? <br>
               2. How many times?

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) { 
        int n = s.length();
        
        for (int i = n / 2; i > 0; i--) {
            if (n % i == 0) {
                int c = n / i;
                StringBuilder sb = new StringBuilder("");
                for (int j = 0; j < c; j++ ) {
                    sb.append(s.substring(0, i));
                }
                if (sb.toString().equals(s)) return true; //这里一定要有sb.toString(), stringbuilder append返回值是object
            }
        }
        
        return false;
    }
}
```
