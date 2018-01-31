[Bold Words in String](https://leetcode.com/problems/bold-words-in-string/description/)

* Solution 1
```java
class Solution {   
    public String boldWords(String[] words, String S) {
          if (words == null || words.length == 0) return "";
          int n = S.length();
          boolean[] mark = new boolean[n];
          
          for (String word: words) {
               markWords(mark, word, S);
          }
          
          StringBuilder sb = new StringBuilder("");
          for (int i = 0; i < S.length(); i++) {
               if (mark[i] && (i == 0 || !mark[i - 1])) {
                    sb.append("<b>");
               }
               sb.append(S.charAt(i));
               if (marked[i] && (i == S.length() - 1 || !marked[i + 1])) {
                    sb.append("</b>");
               }
          }
          return sb.toString();
    }
    private void markWords(boolean[] mark, String word, String S) {
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


