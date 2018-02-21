[Valid Word Abbreviation](https://leetcode.com/problems/valid-word-abbreviation/description/)

```
Given a non-empty string s and an abbreviation abbr, return whether the string matches with the given abbreviation.

A string such as "word" contains only the following valid abbreviations:

["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
Notice that only the above abbreviations are valid abbreviations of the string "word". Any other string is not a valid abbreviation of "word".

Note:
Assume s contains only lowercase letters and abbr contains only lowercase letters and digits.

Example 1:
Given s = "internationalization", abbr = "i12iz4n":

Return true.
Example 2:
Given s = "apple", abbr = "a2e":

Return false.
```

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
            } else {
                if (w[i++] != a[j++]) return false;
            }
        }
        
        return i == w.length && j == a.length;
    }
}
```
