***
```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return helper(root.left, root.right);
    }
    private boolean helper(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        } else if (left == null || right == null) {
            return false;
        }
        return left.val == right.val && helper(left.right, right.left) && helper(left.left, right.right);
    }
}
```
* Solution 2 - 迭代
两种方法：<br>
1. 一个queue，分别加左右孩子. 如果同时为null, continue; "||" -> false, value不相等 -> false. 最后添加左左，右右，左右，右左. <br>
2. 一个stack ... 1. size是奇数肯定false. 2. 每次两个节点一组push到stack. <br>
```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;
   
    Stack<TreeNode> stack = new Stack<TreeNode>();
    stack.push(root.left);
    stack.push(root.right);
    while (!stack.isEmpty()) {
        TreeNode node1 = stack.pop();
        TreeNode node2 = stack.pop();
        if (node1 == null && node2 == null) continue;
        if (node1 == null || node2 == null) return false;
        if (node1.val != node2.val) return false;
        stack.push(node1.left);
        stack.push(node2.right);
        stack.push(node1.right);
        stack.push(node2.left);
    }
    return true;
}
```
