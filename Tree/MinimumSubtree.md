#### Given a binary tree, find the subtree with minimum sum. Return the root of the subtree.
- Example
- Given a binary tree:
```
     1
   /   \
 -5     2
 / \   /  \
0   2 -4  -5
```
return the node 1.

- Solution 1: traverse + divide conquer
```java
public class Solution {
    private TreeNode subtree = null;
    private int subtreeSum = Integer.MAX_VALUE;
    
    public TreeNode findSubtree(TreeNode root) {
        helper(root);
        return subtree;
    }
    
    private int helper(TreeNode root) {
        if (root == null) {
            return 0;
        }
        
        int sum = helper(root.left) + helper(root.right) + root.val;
        if (sum <= subtreeSum) {
            subtreeSum = sum;
            subtree = root;
        }
        return sum;
    }
}
```
- Solution 2: Pure divide conquer
```java
class ResultType {
    public TreeNode minSubtree;
    public int sum, minSum;
    public ResultType(TreeNode minSubtree, int minSum, int sum) {
        this.minSubtree = minSubtree;
        this.minSum = minSum;
        this.sum = sum;
    }
}
public class Solution {
    
    public TreeNode findSubtree(TreeNode root) {
        ResultType result = helper(root);
        return result.minSubtree;
    }
    
    public ResultType helper(TreeNode node) {
        if (node == null) {
            return new ResultType(null, Integer.MAX_VALUE, 0);
        }
        
        ResultType leftResult = helper(node.left);
        ResultType rightResult = helper(node.right);
        
        ResultType result = new ResultType(
            node,
            leftResult.sum + rightResult.sum + node.val,
            leftResult.sum + rightResult.sum + node.val
        );
        
        if (leftResult.minSum <= result.minSum) {
            result.minSum = leftResult.minSum;
            result.minSubtree = leftResult.minSubtree;
        }
        
        if (rightResult.minSum <= result.minSum) {
            result.minSum = rightResult.minSum;
            result.minSubtree = rightResult.minSubtree;
        }
        
        return result;
    }
}
```
