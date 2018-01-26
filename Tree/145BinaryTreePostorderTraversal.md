#1 Iterative Solution using Stack
public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Stack<TreeNode> s = new Stack<>();
        if(root == null) {
            return res;
        }
        s.push(root);   //没有第二选择，初始条件：s为空，root != null；而结束条件一样，无区分度。为了区分开，使其一成为终止条件，必须先push
        while(!s.isEmpty()) {
            TreeNode curr = s.pop();
            res.add(0, curr.val);
            if(curr.left != null) {
                s.push(curr.left);
            }
            if(curr.right != null) {
                s.push(curr.right);
            }
        }
        return res;
}

#2 Recursive Solution is trivial
public List<Integer> postorderTraversal(TreeNode root) {
    List<Integer> res = new ArrayList<>();
    if(root == null) {
        return res;
    }
    helper(root, res);
    return res;
}
public void helper(TreeNode root, List<Integer> res) {
    if(root != null) {
        helper(root.left, res);
        helper(root.right, res);
        res.add(root.val);
    }
}
