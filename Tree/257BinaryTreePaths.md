***
##### Given a binary tree, return all root-to-leaf paths.

* For example, given the following binary tree: <br>
   1 <br>
 /   \ <br>
2     3<br>
 \
  5 <br>
All root-to-leaf paths are: <br>
["1->2->5", "1->3"]
```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        helper(root, res, "");
        return res;
    }
    private void helper(TreeNode root, List<String> res, String path) {
        if (root == null) {
            return ;
        }
        if (root.left == null && root.right == null) {
            res.add(path + root.val);
            return ;
        }
        helper(root.left, res, path + root.val + "->");
        helper(root.right, res, path + root.val + "->");
    }
}
```
