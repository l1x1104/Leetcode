/*
 Date:       Dec 22, 2017
 Update:     Dec 22, 2017
 Problem:    Binary Tree Inorder Traversal
 Difficulty: Easy
 Notes:
 Given a binary tree, return the inorder traversal of its nodes' values.
 For example:
 Given binary tree {1,#,2,3},
 1
  \
   2
  /
 3
 return [1,3,2].
 Note: Recursive solution is trivial, could you do it iteratively?
 Solution: 1. Iterative way (stack).   Time: O(n), Space: O(n).
           2. Recursive solution.      Time: O(n), Space: O(n).
           3. Threaded tree (Morris).  Time: O(n), Space: O(1).
 */
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
#1 Iterative Solution using Stack
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> s = new Stack<>();
        TreeNode curr = root;
        while(!s.isEmpty() || curr != null) {
            while(curr != null) {
                s.push(curr);
                curr = curr.left;
            }
            curr = s.pop();
            res.add(curr.val);
            curr = curr.right;
        }
    }
}

#2 Recursive Solution
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if(root == null) {
            return res;
        }
        helper(root, res);
        return res;
    }
    public void helper(TreeNode root, List<Integer> res) {
        if(root == null) {
            return;
        }
        helper(root.left);
        res.add(root.val);
        helper(root.right);
    }
}

#3 Morris Traversal
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        TreeNode prev = null, curr = root;
        
        while(curr != null) {
            if(curr.left == null) {
                res.add(curr.val);
                curr = curr.right;
            }else {
                prev = curr.left;
                while(prev.right != null && prev.right != curr) prev = prev.right;
                if(prev.right == null) {
                    prev.right = curr;
                    curr = curr.left;
                }else {
                    res.add(curr.val);
                    curr = curr.right;
                    prev.right = null;
                }
            }
        }
        
        return res;
    }
}
