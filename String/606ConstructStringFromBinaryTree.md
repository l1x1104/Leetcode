[Construct String from Binary Tree](https://leetcode.com/problems/construct-string-from-binary-tree/description/)

```java
class Solution {
    public String tree2str(TreeNode t) {
        if (t == null) {
            return "";
        }
        
        String res = t.val + "";
        
        String left = tree2str(t.left);
        String right = tree2str(t.right);
        
        if (left == "" && right == "") {
            return res;
        } else if (left == "") {
            return res + "()" + "(" + right + ")";
        } else if (right == "") {
            return res + "(" + left + ")";
        }
        
        return res + "(" + left + ")" + "(" + right + ")";
    }
}
```
