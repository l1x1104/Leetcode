[Swap Adjacent in LR String](https://leetcode.com/problems/swap-adjacent-in-lr-string/description/)

1. 去掉所有'X'两字符串要长一样 <br>
2. R向右移， L向左移，故start字符串中R必须在end字符串左边，同理L在右边 <br>
Time: O(n) <br>
```java
class Solution {
    public boolean canTransform(String start, String end) {
        if (start.length() != end.length()) {
            return false;
        }
        
        String s = "", e = "";  
        for (int i = 0; i < start.length(); i++)   
            if (start.charAt(i) != 'X')  
                s = s + start.charAt(i);  
        for (int i = 0; i < end.length(); i++)   
            if (end.charAt(i) != 'X')  
                e = e + end.charAt(i);  
        if (!s.equals(e)) {
            return false;  
        }
        
        int l = 0, r = 0;
        for (int i = 0; i < start.length(); i++) {
            if (start.charAt(i) == 'L') l++;
            if (end.charAt(i) == 'L') l--;
            if (start.charAt(i) == 'R') r++;
            if (end.charAt(i) == 'R') r--;
            if (l > 0 || r < 0) return false;
        }
        
        return true;
    }
}
```
