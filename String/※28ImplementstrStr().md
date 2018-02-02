[Implement strStr()](https://leetcode.com/problems/implement-strstr/description/)
- 他山之石 https://discuss.leetcode.com/topic/15569/explained-4ms-easy-c-solution
- Solution 1: brute-force
```java
class Solution {
    public int strStr(String haystack, String needle) {
        int m = haystack.length(), n = needle.length();
        if (n == 0) return 0;
        
        for (int i = 0; i < m - n + 1; i++) {
            int index = 0;
            while (index < n && (haystack.charAt(i + index) == needle.charAt(index))) {
                index ++;
            }
            if (index == n) {
                return i;
            }           
        }
        
        return -1;
        
    }
}
```
- Solution 2: KMP Algo
https://discuss.leetcode.com/topic/10816/kmp-solution-in-java
```java
public class Solution {   
    private int[] failureFunction(char[] str) {
        int[] f = new int[str.length+1];
        for (int i = 2; i < f.length; i++) {
            int j = f[i-1];
            while (j > 0 && str[j] != str[i-1]) j = f[j];
            if (j > 0 || str[j] == str[i-1]) f[i] = j+1;
        }
        return f;
    }

    public int strStr(String haystack, String needle) {
        if (needle.length() == 0) return 0;
        if (needle.length() <= haystack.length()) {
            int[] f = failureFunction(needle.toCharArray());
            int i = 0, j = 0;
            while (i < haystack.length()) {
                if (haystack.charAt(i) == needle.charAt(j)) {
                    i++; j++;
                    if (j == needle.length()) return i-j;
                } else if (j > 0) j = f[j];
                else i++;
            }
        }
        return -1;
    }
}
```
