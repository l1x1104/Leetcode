[Valid Word Abbreviation](https://leetcode.com/problems/valid-word-abbreviation/description/)

```java
class Solution {
    public boolean validWordAbbreviation(String word, String abbr) {
        int number = 0, i = 0, j = 0;
        while (i < word.length() && j < abbr.length()) {
            if (Character.isDigit(abbr.charAt(j))) {
                number = number * 10 + abbr.charAt(j) - '0';
                if (number == 0) return false;
                j++;
            } else {
                i += number;
                if (i >= word.length() || word.charAt(i) != abbr.charAt(j)) return false;
                number = 0;
                i++; 
                j++;
            }
        }
        i += number;
        return i == word.length() && j == abbr.length();       
    }
}
```
