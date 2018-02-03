[回文子字符串](https://leetcode.com/problems/palindromic-substrings/description/)

- Solution 1: brute - force
```java
class Solution {
    private int res = 0;
    public int countSubstrings(String s) {
        int n = s.length();
        char[] ch = s.toCharArray();
        
        for (int i = 0; i < ch.length; i++) {
            helper(ch, i, i);
            helper(ch, i, i + 1);
        }
        
        return res;
    }
    private void helper(char[] ch, int i, int j) {
        while (i >= 0 && j < ch.length && ch[i--] == ch[j++]) {
            res++;
        }
    }
}
```

- Solution 2: DP
