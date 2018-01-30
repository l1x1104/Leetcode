[Path Sum](https://leetcode.com/problems/path-sum/description/)
* Solution 1 - Recursive
```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        if (sum == root.val && root.left == null && root.right == null) {
            return true;
        }
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
    
}
```

* Solution 2 - Iterative
```java
public boolean hasPathSum(TreeNode root, int sum) {
    Stack <TreeNode> stack = new Stack<> ();	    
	  stack.push(root) ;	    
	  while (!stack.isEmpty() && root != null) {
	      TreeNode cur = stack.pop() ;	
	    	if (cur.left == null && cur.right == null){	    		
	    	    if (cur.val == sum ) {
                return true ;
            }
	    	}
	    	if (cur.right != null) {
	    		cur.right.val = cur.val + cur.right.val ;
	    		stack.push(cur.right) ;
	    	}
	    	if (cur.left != null) {
	    		cur.left.val = cur.val + cur.left.val;
	    		stack.push(cur.left);
	    	}
	  }	    
    return false ;
}
```
