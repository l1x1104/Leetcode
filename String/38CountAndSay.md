[Count And Say](https://leetcode.com/problems/count-and-say/description/)

```java
class Solution {
    public String countAndSay(int n) {
        String str = "1";
        if (n == 1) {
            return str;
        }
        
        for(int i = 1; i < n; i++){
            str = helper(str);
        }
        
        return str;
    }
    
    private String helper(String str) {
        StringBuilder sb = new StringBuilder("");
        int i = 0;
        
        while (i < str.length()) {
            int j = i, len = 0;
            while (j < str.length() && str.charAt(j) == str.charAt(i)) {
                j ++;
            }
            len = j - i;
            sb.append(len);
            sb.append(str.charAt(i));
            i = j;
        }
        
        return sb.toString();
    }
}
```
