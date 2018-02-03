[ZigZag Conversion](https://leetcode.com/problems/zigzag-conversion/description/)

```java
class Solution {
    public String convert(String s, int numRows) {
        char[] ch = s.toCharArray();
        int n = ch.length;
        StringBuffer[] sb = new StringBuffer[numRows];
        for (int i = 0; i < sb.length; i++) sb[i] = new StringBuffer();
        
        int idx = 0 ;
        while (idx < n) {
            for (int i = 0; i < numRows && idx < n; i++) // vertically down
                sb[i].append(ch[idx++]);
            for (int j = numRows - 2; j >= 1 && idx < n; j--) // obliquely up
                sb[j].append(ch[idx++]);
        }
        for (int i = 1; i < sb.length; i++) {
            sb[0].append(sb[i]);
        }
        
        return sb[0].toString();
    }
}
```
