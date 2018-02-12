[调整屏幕上的句子](https://leetcode.com/problems/sentence-screen-fitting/description/)

```java
class Solution {
    public int wordsTyping(String[] sentence, int rows, int cols) {
        String s = "";
        for (String str: sentence) {
            s += str + " ";
        }
        
        int start = 0, n = s.length();
        for (int i = 0; i < rows; i++) {
            start += cols;
            if (s.charAt(start % n) == ' ') {
                start++;
            } else {
                while (start > 0 && s.charAt((start - 1) % n) != ' ') {
                    start--;
                }
            }
        }
        
        return start / n;
    }
}
```
