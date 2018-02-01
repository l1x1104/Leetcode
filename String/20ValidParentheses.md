[Valid Parentheses](https://leetcode.com/problems/valid-parentheses/description/)

* Solution 1 - one stack
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
	      for (char c : s.toCharArray()) {
		    if (c == '(')
			    stack.push(')');
		    else if (c == '{')
			    stack.push('}');
		    else if (c == '[')
			    stack.push(']');
		    else if (stack.isEmpty() || stack.pop() != c)
			    return false;  
	      }
	    return stack.isEmpty();
    }
}
```

Solution 2 - array
