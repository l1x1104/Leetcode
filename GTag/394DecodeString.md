[解码字符串](https://leetcode.com/problems/decode-string/discuss/)

```java
class Solution {
    public String decodeString(String s) {
        Stack<Integer> numbers = new Stack<>();
        Stack<String> result = new Stack<>();
        
        int i = 0;
        result.push("");
        char[] ch = s.toCharArray();
        
        while (i < ch.length) {
            char c = ch[i];
            if (Character.isDigit(c)) {
                int num = c - '0';
                while (Character.isDigit(ch[i + 1])) {
                    num = num * 10 + ch[i + 1] - '0';
                    i++;
                }
                numbers.push(num);
            } else if (c == '[') {
                result.push("");
            } else if (c == ']') {
                String str = result.pop();
                StringBuilder sb = new StringBuilder();
                int t = numbers.pop();
                for (int j = 0; j < t; j++) {
                    sb.append(str);
                }
                result.push(result.pop() + sb.toString());
            } else {
                result.push(result.pop() + ch[i]);
            }
            i++;
        }
        
        return result.pop();
    }
}
```
