/*
 Date:       Dec 25, 2017
 Update:     Dec 25, 2017
 Problem:    Find Leaves of Binary Tree
 Difficulty: Medium
 Notes:
 Given a binary tree, collect a tree's nodes as if you were doing this: Collect and remove all leaves, repeat until the tree is
 empty.
 For example:
 Given binary tree {1,#,2,3},
          1
         / \
        2   3
       / \     
      4   5    
 Returns [4, 5, 3], [2], [1].
 Note: Recursive solution is trivial, could you do it iteratively?
 Solution: 1. Recursive solution.      Time: O(2n), Space: O(n).
 */
 ```java
 class Solution {
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Map<TreeNode, Integer> map = new HashMap<>();
        int num = dfs(root, map);
        for(int i = 0; i < num; i++) {
            res.add(new ArrayList<>());
        }
        helper(root, res, map);
        return res;
    }
    private int dfs(TreeNode root, Map<TreeNode, Integer> map) {
        if(root == null) return 0;
        int left = dfs(root.left, map);
        int right = dfs(root.right, map);
        map.put(root, Math.max(left, right));
        return 1 + Math.max(left, right);
    }
    private void helper(TreeNode root, List<List<Integer>> res, Map<TreeNode, Integer> map) {
        if(root == null) return ;
        helper(root.left, res, map);
        helper(root.right, res, map);
        int level = map.get(root);
        List<Integer> tmp = res.get(level);
        tmp.add(root.val);
    }
  }
  ```
  这题的解释非常棒 https://discuss.leetcode.com/topic/49194/10-lines-simple-java-solution-using-recursion-with-explanation <br>
  The key is to find the height of each node. Here the definition of height is: The height of a node is the number of edges    from the node to the deepest leaf
  
  ```java
  class Solution {
    public List<List<Integer>> findLeaves(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        height(root, res);
        return res;
    }
    private int height(TreeNode node, List<List<Integer>> res){
        if (null == node)  return -1;
        int level = 1 + Math.max(height(node.left, res), height(node.right, res));
        if(res.size() < level + 1)  res.add(new ArrayList<>());
        res.get(level).add(node.val);
        node.left = node.right = null;
        return level;
    }
 }
  ```
