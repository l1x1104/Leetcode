[Basic Calculator II](https://leetcode.com/problems/basic-calculator-ii/description/)

```java
class Solution {
    public int calculate(String s) {
        s = s.trim();
        int n = s.length();
        if(s == null || n == 0) {
            return 0;
        }
        
        int num = 0;
        char sign = '+';
        Stack<Integer> stack = new Stack<>();
        char[] ch = s.toCharArray();
        for (int i = 0; i < n; i++) {
            if(Character.isDigit(ch[i])){
                num = num * 10 + ch[i]-'0';
            }
            if (!Character.isDigit(ch[i]) && ch[i] != ' ' || i == n - 1) {
                if(sign == '-'){
                    stack.push(-num);
                }
                if(sign == '+'){
                    stack.push(num);
                }
                if(sign == '*'){
                    stack.push(stack.pop() * num);
                }
                if(sign == '/'){
                    stack.push(stack.pop() / num);
                }
                sign = ch[i];
                num = 0;
            }
        }
        
        int res = 0;
        for (Integer i: stack) {
            res += i;
        }
        
        return res;                  
    }
}
```
