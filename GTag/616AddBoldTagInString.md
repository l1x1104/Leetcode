[字符串中增添加粗标签](https://leetcode.com/problems/add-bold-tag-in-string/description/)

```java
class Solution {
    public String addBoldTag(String s, String[] dict) {
        int n = s.length();
        if (s == null || n == 0) return "";
        
        boolean[] mark = new boolean[n];
        for (String word: dict) {
            markWords(mark, word, s);
        }
        
          StringBuilder sb = new StringBuilder("");
          for (int i = 0; i < n; i++) {
               if (mark[i] && (i == 0 || !mark[i - 1])) {
                    sb.append("<b>");
               }
               sb.append(s.charAt(i));
               if (mark[i] && (i == n - 1 || !mark[i + 1])) {
                    sb.append("</b>");
               }
          }
          return sb.toString();        
    }
    
    private void markWords(boolean[] marked, String word, String S) {
          for (int i = 0; i <= S.length() - word.length(); i++) {
            String substr = S.substring(i, i + word.length());
            if (substr.equals(word)) {
                for (int j = i; j < i + word.length(); j++) {
                    marked[j] = true;
                }
            }
         }
    }
}
```
