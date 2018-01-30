#### Given a binary tree, you need to find the length of Longest Consecutive Path in Binary Tree. Especially, this path can be either increasing or decreasing. For example, [1,2,3,4] and [4,3,2,1] are both considered valid, but the path [1,2,4,3] is not valid. On the other hand, the path can be in the child-Parent-child order, where not necessarily be parent-child order.

* Example 1:
- Input:
```
        1
       / \
      2   3
```      
Output: 2 <br>
Explanation: The longest consecutive path is [1, 2] or [2, 1]. <br>
* Example 2:
- Input:
```
        2
       / \
      1   3
```
Output: 3 <br>
Explanation: The longest consecutive path is [1, 2, 3] or [3, 2, 1]. 
- Note: All the values of tree nodes are in the range of [-1e7, 1e7].

```java
public class Solution {
    int max = 0;
    
    class Result {
        TreeNode node;
        int inc;
        int des;
        public Result(TreeNode node, int inc, int des) {
            this.node = node;
            this.inc = inc;
            this.des = des;
        }
    }
    
    public int longestConsecutive(TreeNode root) {
        traverse(root);
        return max;
    }
    
    private Result traverse(TreeNode node) {
        if (node == null) return null;
        
        Result left = traverse(node.left);
        Result right = traverse(node.right);
        
        Result curr = new Result(node, 1, 1);
        
        if (left != null) {
            if (node.val - left.node.val == 1) {
                curr.inc = Math.max(curr.inc, left.inc + 1);
            }else if (node.val - left.node.val == -1) {
                curr.des = Math.max(curr.des, left.des + 1);
            }
        }
        
        if (right != null) {
            if (node.val - right.node.val == 1) {
                curr.inc = Math.max(curr.inc, right.inc + 1);
            }else if (node.val - right.node.val == -1) {
                curr.des = Math.max(curr.des, right.des + 1);
            }
        }
        
        max = Math.max(max, curr.inc + curr.des - 1);
        
        return curr;
    }
}
```
