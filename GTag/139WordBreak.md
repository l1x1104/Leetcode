[拆分词句](https://leetcode.com/problems/word-break/description/)

```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int n = s.length();
        if (s == null || n == 0) {
            return true;
        }       
        boolean[] result = new boolean[n + 1];
        result[0] = true;
        
        for (int i = 0; i < n; i++) {
            StringBuilder sb = new StringBuilder(s.substring(0, i + 1));
            for (int j = 0; j<= i; j++) {
                if (result[j] && wordDict.contains(sb.toString())) {
                    result[i + 1] = true;
                    break;
                }
                sb.deleteCharAt(0);
            }
        }
        
        return result[n];
    }
}
```
