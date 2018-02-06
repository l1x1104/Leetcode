[验证括号字符串](https://leetcode.com/problems/valid-parenthesis-string/description/)

Note: 重点考虑这两栗子 ' *) ' (可以)和 ' *( ' (🚫)
- Solution 1: Time O(n) Space O(1)
```java
class Solution {
    public boolean checkValidString(String s) {
        Stack<Integer> left = new Stack<>();
        Stack<Integer> star = new Stack<>();
        
        char[] ch = s.toCharArray();
        for (int i = 0 ; i < ch.length; i++) {
            char c = ch[i];
            if (c == '*') star.push(i);
            else if (c == '(') {
                left.push(i);
            } else {
                if (left.isEmpty() && star.isEmpty()) return false;
                else if (!left.isEmpty()) {
                    left.pop();
                } else {
                    star.pop();
                }
            }
        }
        
        while (!left.isEmpty() && !star.isEmpty()) {
            if (left.peek() > star.peek()) return false;
            left.pop(); 
            star.pop();
        }
        
        return left.isEmpty();        
    }
}
```
