   * Solution 1 - Iterative
   ```java
   public boolean isValidBST(TreeNode root) {
        Stack<TreeNode> s = new Stack<>();
        TreeNode curr = root;
        TreeNode prev = null;
        
        while(!s.isEmpty() || curr != null) {
            while(curr != null) {
                s.push(curr);
                curr = curr.left;
            }
            curr = s.pop();
            if(prev != null && prev.val >= curr.val) {
                return false;
            }
            prev = curr;
            curr = curr.right;
        }
        return true;
    }
```
    
* Solution 2 - Recursive
recursively iterating over the tree while defining interval <minVal, maxVal> for each node which value must fit in.
```java
public boolean isValidBST(TreeNode root) {
    return isValidBST(root, Long.MIN_VALUE, Long.MAX_VALUE);
}
    
public boolean isValidBST(TreeNode root, long minVal, long maxVal) {
    if (root == null) return true;
    if (root.val >= maxVal || root.val <= minVal) return false;
        return isValidBST(root.left, minVal, root.val) && isValidBST(root.right, root.val, maxVal);
}
```
