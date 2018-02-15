[验证缩写](https://leetcode.com/problems/valid-word-abbreviation/description/)

```java
class Solution {
    public boolean validWordAbbreviation(String word, String abbr) {
        int i = 0, j = 0;
        char[] w = word.toCharArray();
        char[] a = abbr.toCharArray();
        
        while (i < w.length && j < a.length) {
            char c = a[j];
            if (Character.isDigit(c)) {
                if (a[j] == '0') return false;
                int number = 0;
                while (j < a.length && Character.isDigit(a[j])) {
                    number = number * 10 + a[j] - '0';
                    j ++;
                }
                i += number;
                System.out.println("number=" + number);
            } else {
                System.out.println("i" + i + ",  j" + j);
                if (w[i++] != a[j++]) return false;
            }
        }
        
        return i == w.length && j == a.length;
    }
}
```
