[Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

- Solution 1: Traverse
```java
class Solution {
        public List<Integer> postorderTraversal(TreeNode root) {
                List<Integer> result = new ArrayList<Integer>();
                Stack<TreeNode> stack = new Stack<TreeNode>();
                TreeNode prev = null; // previously traversed node
                TreeNode curr = root;

                if (root == null) {
                        return result;
                }

                stack.push(root);
                while (!stack.empty()) {
                        curr = stack.peek();
                        if (prev == null || prev.left == curr || prev.right == curr) { // traverse down the tree
                                if (curr.left != null) {
                                        stack.push(curr.left);
                                } else if (curr.right != null) {
                                        stack.push(curr.right);
                                }
                        } else if (curr.left == prev) {
                                if (curr.right != null) {
                                        stack.push(curr.right);
                                }
                        } else { 
                                result.add(curr.val);
                                stack.pop();
                        }
                        prev = curr;
                }

                return result;
        }
}
```

- Solution 2 Divide & Conquer
```java
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<Integer>();

        if (root == null) {
                return result;
        }

        result.addAll(postorderTraversal(root.left));
        result.addAll(postorderTraversal(root.right));
        result.add(root.val);

        return result;   
    }
}
```

