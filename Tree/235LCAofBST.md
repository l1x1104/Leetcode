BST的好处就是快速决定左右子树是否存在，或者在左、右分支.

```java
   public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode m = root;
        if(m.val > p.val && m.val < q.val){
            return m;  
        }else if(m.val>p.val && m.val > q.val){
            return lowestCommonAncestor(root.left, p, q);
        }else if(m.val<p.val && m.val < q.val){
            return lowestCommonAncestor(root.right, p, q);
        }
 
        return root;    
    }
```

#### 236. Lowest Common Ancestor of a Binary Tree 这题没有二分的便利条件，只能从bottom开始根据上一层返回值判断.
```java
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == p || root == q || root == null)
            return root;
        TreeNode left = lowestCommonAncestor( root.left,  p,  q);
        TreeNode right = lowestCommonAncestor( root.right,  p,  q);
        if(left == null)
            return right;
        else if (right == null)
            return left;
        else
            return root;
        
    }
```
