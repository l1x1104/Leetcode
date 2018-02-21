[验证括号字符串](https://leetcode.com/problems/valid-parenthesis-string/description/)

Note: 重点考虑这两栗子 ' *) ' (可以)和 ' *( ' (🚫不可以)
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

- Solution 2: 递归
```java
class Solution {   
    public boolean checkValidString(String s) {
        return helper(0, 0, s);
    } 
    
    private boolean helper(int start, int cnt, String str) {
        if (cnt < 0) return false;
        for (int i = start; i < str.length(); i++) {
            char c = str.charAt(i);
            if (c == '(') {
                cnt ++;
            } else if (c == ')') {
                if (cnt <= 0) return false;
                cnt --;
            } else {
                return helper(i + 1, cnt, str) || helper(i + 1, cnt + 1, str) || helper(i + 1, cnt - 1, str);
            }
        }       
        return cnt == 0;
    }
}
```

- Solution 3: 他山之石
这里维护了两个变量low和high，其中low表示在有左括号的情况下，将星号当作右括号时左括号的个数(这样做的原因是尽量不多增加右括号的个数)，而high表示将星号当作左括号时左括号的个数。是不是很绕，没办法。那么当high小于0时，说明就算把星号都当作左括号了，还是不够抵消右括号，返回false。而当low大于0时，说明左括号的个数太多了，没有足够多的右括号来抵消，返回false。那么开始遍历字符串，当遇到左括号时，low和high都自增1；当遇到右括号时，只有当low大于0时，low才自减1，保证了low不会小于0，而high直接自减1；当遇到星号时，只有当low大于0时，low才自减1，保证了low不会小于0，而high直接自增1，因为high把星号当作左括号。当此时high小于0，说明右括号太多，返回false。当循环退出后，我们看low是否为0
```java
class Solution {   
    public boolean checkValidString(String s) {
        int low = 0, high = 0;
        char[] ch = s.toCharArray();
        for (Character c : ch) {
            if (c == '(') {
                ++low; 
                ++high;
            } else if (c == ')') {
                if (low > 0) --low;
                --high;
            } else {
                if (low > 0) --low;
                ++high;
            }
            
            if (high < 0) return false;
        }
        return low == 0;
    }     
}
```
