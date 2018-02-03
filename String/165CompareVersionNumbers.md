[Compare Version Numbers](https://leetcode.com/problems/compare-version-numbers/description/)

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        int m = version1.length(), n = version2.length();
        int i = 0, j = 0, d1 = 0, d2 = 0;
        String v1, v2;
        
        while (i < m || j < n) {            
            while (i < m && version1.charAt(i) != '.') {
                d1 = d1 * 10 + version1.charAt(i++) - '0';
            }
            while (j < n && version2.charAt(j) != '.') {
                d2 = d2 * 10 + version2.charAt(j++) - '0';
            }
            if (d1 > d2) {
                return 1;
            } else if (d1 < d2) {
                return -1;
            }
            d1 = 0; d2 = 0; i++; j++;
        }
        
        return 0;
    }
}
```
