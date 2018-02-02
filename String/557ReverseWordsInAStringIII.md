[Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/description/)

```java
class Solution {
    public String reverseWords(String str) {
        char[] ch = str.toCharArray();
        int begin = 0;
        
        for (int i = 0; i < ch.length; i++) {
            if (ch[i] == ' ') {
                reverse(ch, begin, i - 1);
                begin = i + 1;
            }
        }
        reverse(ch, begin, ch.length - 1);
        return new String(ch);
    }
    private void reverse(char[]ch, int i, int j) {
        while (i <= j) {
            char temp = ch[i];
            ch[i++] = ch[j];
            ch[j--] = temp;
        }
    }
}
```
