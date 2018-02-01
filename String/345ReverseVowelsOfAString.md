[Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/description/)

```java
class Solution {
    public String reverseVowels(String s) {
        Stack<Character> stack = new Stack<>();
        String t = "aeiouAEIOU";
        
        char[] str = s.toCharArray();
        for (int x = 0; x < str.length; x++) {
            if (t.contains(String.valueOf(str[x]))) stack.push(str[x]);
        } 
        
        StringBuilder sb = new StringBuilder();
        for (int y = 0; y < str.length; y++) {
            if (t.contains(String.valueOf(str[y]))) {
                sb.append(stack.pop());
            } else {
                sb.append(str[y]);
            }
        }
        
        return sb.toString();
    }
}
```
