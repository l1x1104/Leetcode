```java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        TreeNode rst = null;
        if(t1 == null) {
            return t2;
        }else if(t2 == null) {
            return t1;
        }
        rst = new TreeNode(t1.val + t2.val);
        rst.left = mergeTrees(t1.left, t2.left);
        rst.right = mergeTrees(t1.right, t2.right);
        
        return rst;
    }
}
```
