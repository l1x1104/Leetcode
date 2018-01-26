[Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

- Solution 1: Traverse
```java
public class Solution {
    /**
     * @param root: The root of binary tree.
     * @return: Inorder in ArrayList which contains node values.
     */
    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        Stack<TreeNode> stack = new Stack<TreeNode>();
        ArrayList<Integer> result = new ArrayList<Integer>();
        TreeNode curt = root;
        while (curt != null || !stack.empty()) {
            while (curt != null) {
                stack.add(curt);
                curt = curt.left;
            }
            curt = stack.pop();
            result.add(curt.val);
            curt = curt.right;
        }
        return result;
    }
}
```

- Solution 2 Divide & Conquer
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();
        // null or leaf
        if (root == null) {
            return result;
        }

        // Divide
        List<Integer> left = inorderTraversal(root.left);
        List<Integer> right = inorderTraversal(root.right);

        // Conquer
        result.addAll(left);
        result.add(root.val);
        result.addAll(right);
        return result;    
    }
}
```

- Solution 3 Morris Traversal
```java
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        TreeNode prev = null, curr = root;
        
        while(curr != null) {
            if(curr.left == null) {
                result.add(curr.val);
                curr = curr.right;
            }else {
                prev = curr.left;
                while(prev.right != null && prev.right != curr) prev = prev.right;
                if(prev.right == null) {
                    prev.right = curr;
                    curr = curr.left;
                }else {
                    result.add(curr.val);
                    curr = curr.right;
                    prev.right = null;
                }
            }
        }
        
        return result;
    }
}
```
