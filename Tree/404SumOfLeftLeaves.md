#### Straightforward Solution
```java
int sum;
public int sumOfLeftLeaves(TreeNode root) {
    sum = 0;
    inOrder(root, false); // false means the next node is not in the left side.
    
    return sum;
}

private void inOrder(TreeNode root, boolean left) {
    if (root == null) {
        return;
    }

    inOrder(root.left, true); // true means the next node is in the left side.
    if (root.left == null && root.right == null && left) { // only left leaves can be added to result;
        sum += root.val;
    }
    inOrder(root.right, false);
}
```

#### Solution 2 - Iterative
```java
public class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        if(root == null || root.left == null && root.right == null) return 0;
        
        int res = 0;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while(!queue.isEmpty()) {
            TreeNode curr = queue.poll();

            if(curr.left != null && curr.left.left == null && curr.left.right == null) res += curr.left.val;
            if(curr.left != null) queue.offer(curr.left);
            if(curr.right != null) queue.offer(curr.right);
        }
        return res;
    }
}
```
