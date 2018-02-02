[Count Binary Substrings](https://leetcode.com/problems/count-binary-substrings/description/)
字符串的题目如果不想得出暴力解就要仔细观察规律
```java
class Solution {
    public int countBinarySubstrings(String s) {
        int index = 0, prevNumber = 0, res = 0;
        
        while (index < s.length()) {
            char prev = s.charAt(index);
            int number = 0;
            while (index < s.length() && s.charAt(index) == prev) {
                number ++;
                index ++;
            }
            if (prevNumber != 0 ) {
                res += Math.min(prevNumber, number);
            }
            prevNumber = number;
        }
        
        return res;
    }
}
```
