[Path Sum II](https://leetcode.com/problems/path-sum-ii/description/)
- Solution 1 Traverse
```java
如果postorder做把line83换到line85之后即可。
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        helper(root, sum, 0, tmpList, res);
        return res;
    }
    public void helper(TreeNode root, int target, int sum, List<Integer> tmpList, List<List<Integer>> res) {
        if(root == null) return;
        tmpList.add(root.val);
        if((sum + root.val == target) && root.left == null && root.right == null) res.add(new ArrayList<>(tmpList)); 
        helper(root.left, target, sum + root.val, tmpList, res);
        helper(root.right, target, sum + root.val, tmpList, res);
        tmpList.remove(tmpList.size() - 1);
    }
}
```
