[Verify Preorder Serialization of a Binary Tree](https://leetcode.com/problems/verify-preorder-serialization-of-a-binary-tree/description/)

```java
class Solution {
    public boolean isValidSerialization(String preorder) {
        String[] ch = preorder.split(",");
        if (ch.length == 0) {
            return true;
        }
        
        Stack<String> stack = new Stack<>();
        for (int i = 0; i < ch.length; i++) { 
            while (ch[i].equals("#") && !stack.isEmpty() && stack.peek().equals("#")) {
                stack.pop();
                if (stack.isEmpty()) {
                    return false;
                }
                stack.pop();
            }
            
             stack.push(ch[i]);
        }
        
        return stack.size() == 1 && stack.peek().equals("#");
    }
}
```
