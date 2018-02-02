[Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/description/)
自己想到的是思路是每个string做一次substring，对每一个string时间: O(1 + 2 + 3 .. + n) = O(n), 比较下一个string是否contains这个substring,取最长的substring. 所以总时长就是O(m * n), m是平均每个string的长度,n是输入string[]长度.
- 关键词：longest, prefix(start from index 0)
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        // "abcdefgh", "aefghijk", "abcefgh"
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
