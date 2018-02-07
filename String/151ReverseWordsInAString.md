[Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/description/)
```
Input:
"   a   b "
Output:
"b   a"
Expected:
"b a"
```
- Solution 1
```java
public class Solution {
    public String reverseWords(String s){
        s = s.trim();
        String[] str = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for(int i = str.length - 1;i >= 0; i --) {
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
        if (s.length() < 1) return s;
  
        char[] ch = s.toCharArray();
        reverse(ch, 0, ch.length - 1);
        
        int storedIndex = 0;
        for (int i = 0; i < ch.length; i++) {
            if (ch[i] != ' ') {
                if (storedIndex != 0) ch[storedIndex++] = ' ';
                int j = i;
                while (j < ch.length && ch[j] != ' ') {
                    ch[storedIndex++] = ch[j++];
                }
                reverse(ch, storedIndex - (j - i), storedIndex - 1);
                i = j;
            }
        }
        
        return new String(ch, 0, storedIndex);
    }
    
    private void reverse(char[] ch, int start, int end) {
        for (; start < end; start ++, end --) {
            char tmp = ch[end];
            ch[end] = ch[start];
            ch[start] = tmp;
        }
    }
}
```
