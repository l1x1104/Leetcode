[迷你解析器](https://leetcode.com/problems/mini-parser/description/)
1. deserialize用到string方法. 2. implement interface用到oop知识
```java
public NestedInteger deserialize(String s) {

    // "[123,[456,[789]]]"
    
    if (s.isEmpty()) return null;
    if (s.charAt(0) != '[') {
        return new NestedInteger(Integer.valueOf(s));
    }
    
    Stack<NestedInteger> stack = new Stack<>();    
    NestedInteger curr = null;
    int l = 0;  
    for (int r = 0; r < s.length(); r++) {
        char ch = s.charAt(r);
        if (ch == '[') {
            if (curr != null) {
                stack.push(curr);
            }
            curr = new NestedInteger();
            l = r + 1;
        } else if (ch == ',') {
            if (s.charAt(r - 1) != ']') {
                String number = s.substring(l, r);
                curr.add(new NestedInteger(Integer.valueOf(number)));
            }
            l = r + 1;
        } else if (ch == ']') {
            String number = s.substring(l, r);
            if (!number.isEmpty()) {
                curr.add(new NestedInteger(Integer.valueOf(number)));
            }
            if (!stack.isEmpty()) {
                NestedInteger pop = stack.pop();
                pop.add(curr);
                curr = pop;
            }
            l = r + 1;
        }
       
    }
    
    return curr;
}
```
