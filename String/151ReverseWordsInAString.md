[Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)

- Solution 1
```java
public class Solution {
    public String reverseWords(String s){
        s = s.trim();
        String[] str = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for(int i = str.length -1;i >= 0; i --) {
            String tmp = str[i].trim();
            if (tmp.equals("")) {
                continue;
            }
            sb.append(tmp);
            if(i > 0) {
                sb.append(" ");
            }
        }
        return sb.toString();
    }
}
```

- Solution 2 in-place
```java
public class Solution {
    public String reverseWords(String s) {
        if (s.length() < 1) return s; // empty string
        int startIdx = 0;
        char[] str = s.toCharArray();
        // reverse whole string
        reverse(str, 0, str.length - 1);
        // reverse word one by one
        for (int i = 0; i < str.length; i++) {
            if (str[i] != ' ') {
                if (startIdx != 0) str[startIdx++] = ' ';
                int j = i;
                while (j < str.length && str[j] != ' ') str[startIdx++] = str[j++];
                reverse(str, startIdx - (j - i), startIdx - 1); 
                i = j;
            }
        }
        return new String(str, 0, startIdx);
    }

    private void reverse(char[] str, int begin, int end) {
        for (; begin < end; begin++, end--) {
            char tmp = str[begin];
            str[begin] = str[end];
            str[end] = tmp;
        }
    }
}
```
