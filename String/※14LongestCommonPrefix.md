[Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/) <br>
Example: "abcdefgh", "aefghijk", "abcefgh" <br>
- 关键词：longest, prefix(start from index 0)
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs == null || strs.length == 0) {
            return "";
        }
        
        int i = 1;
        String pre = strs[0];     
        while(i < strs.length){
            while(strs[i].indexOf(pre) != 0) {
                pre = pre.substring(0,pre.length() - 1);
            }
            i++;
        }
        
        return pre;
    }
}
```
