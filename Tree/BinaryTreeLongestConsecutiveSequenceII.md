#### Given a binary tree, find the length of the longest consecutive sequence path. The path could be start and end at any node in the tree
* Example
```
    1
   / \
  2   0
 /
3
```
Return 4 // 0-1-2-3
```java
public class Solution {
    private int path = 0;
    public class Result{
        TreeNode prevNode;
        int decrease, increase;
        public Result(TreeNode node, int decrease, int increase) {
            this.prevNode = node;
            this.decrease = decrease;
            this.increase = increase;
        }
    }
    
    public int longestConsecutive2(TreeNode root) {
        // write your code here
        if (root == null) {
            return 0;
        }
        
        // Divide & Conquer + traverse
        helper(root);
        return path;
    }
    private Result helper(TreeNode root) {
        if (root == null) {
            return new Result(null, 0, 0);
        }
        Result left = helper(root.left);
        Result right = helper(root.right);
        
        int lD = left.decrease, rD = right.decrease;
        int lI = left.increase, rI = right.increase;
        int dec = 1, inc = 1;
        
        if (left.prevNode != null) {
            if (left.prevNode.val == root.val + 1) {
                dec = lD + 1;
            } else if (left.prevNode.val == root.val - 1) {
                inc = lI + 1;
            }
        }
        
        if (right.prevNode != null) {
            if (right.prevNode.val == root.val + 1) {
                dec = Math.max(dec, rD + 1);
            } else if (right.prevNode.val == root.val - 1) {
                inc = Math.max(inc, rI + 1);
            }
        }
        
        path = Math.max(path, inc + dec - 1);
        
        return new Result(root, dec, inc);
    }
}
```
