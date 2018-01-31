[Repeated String Match](https://leetcode.com/problems/repeated-string-match/description/)

* Solution 1 <br>
B is a substring of A, A.length >= B.length <br>
```java
class Solution {
    public int repeatedStringMatch(String A, String B) {
        int count = 0;
        StringBuilder t = new StringBuilder("");
        
        while (t.length() < B.length()) {
            t.append(A);
            count ++;
        }
        
        if (t.toString().contains(B)) return count;
        t.append(A);
        return t.toString().contains(B) ? ++count: -1;
    }
}
```

* Solution 2 <br>
没有用到built-in函数. <br>
从A中取字符把A当作一个循环数组来处理，用(i+j)%m来取字符，且确保j小于n，避免越界，如果字符匹配的话，j自增1. while 循环结束后，如果j等于n了，说明B中所有的字符都成功匹配了，我们来计算A的重复次数，通过(i+j-1)/m + 1来得到.注意i+j要减1再除以m，之后再加上一次. 因为当i+j正好等于m时，说明此时不用重复A，那么(i+j-1)/m + 1还是等于1;当i+j>m的时候，需要重复A了，(i+j-1)/m + 1也可以得到正确的结果.
```java
class Solution {
    public int repeatedStringMatch(String A, String B) {
        int m = A.length(), n = B.length();
        
        for (int i = 0; i < m; i++) {
            int j = 0;
            while (j < n && A.charAt((i + j) % m) == B.charAt(j)) {
                j++;
            }
            
            if (j == n) {
                return (i + j - 1) / m + 1;
            }
        }
        
        return -1;
    }
}
```
