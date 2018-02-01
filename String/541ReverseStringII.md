[Reverse String II](https://leetcode.com/problems/reverse-string-ii/description/)

```java
class Solution {
    public String reverseStr(String s, int k) {
        char[] ch = s.toCharArray();
        for (int i = 0; i < ch.length; i += k * 2) {
            reverse(ch, i, i + k);
        }
        return String.valueOf(ch);
    }
    private void reverse(char[] ch, int i, int j) {
        j = Math.min(ch.length, j) - 1;
        for (; i < j; i++, j--) {
            char tmp = ch[i];
            ch[i] = ch[j];
            ch[j] = tmp;
        }
    }
}
```
