[删除后得到的字典中的最长单词](https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/)


```java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        if (s.length() == 0 || d.size() == 0) {
            return "";
        }
        
        Collections.sort(d, new Comparator<String>() {
            @Override
            public int compare(String a, String b) {
                if (a.length() == b.length()) {
                    return a.compareTo(b);
                }
                return b.length() - a.length();
            }
        });
        
        for (String str: d) {
            if (str.length() > s.length()) {
                continue;
            }
            if (subSequence(str, s)) {
                return str;
            }
        }
        
        return "";
    }
    
    private boolean subSequence(String sub, String s) {
        int i = 0, j = 0;
        while (i < s.length() && j < sub.length()) {
            if (s.charAt(i) == sub.charAt(j)) {
                j++;
            }
            i++;
        }
        return j == sub.length();
    }    
}
```

```java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        if (s.length() == 0 || d.size() == 0) {
            return "";
        }
        
        String result = "";
        char[] ch = s.toCharArray();
        for (String str: d) {
            int i = 0;
            for (Character c: ch) {
                if (i < str.length() && str.charAt(i) == c) {
                    i++;
                }
            }
            if (i == str.length() && str.length() >= result.length()) {
                if (str.length() > result.length() || str.compareTo(result) < 0) {
                    result = str;
                }
            }
        }
        
        return result;
    }
}
```
