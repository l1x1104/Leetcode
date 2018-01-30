#### Given a binary tree, find the length of the longest consecutive sequence path. The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).
- Example
- Given a binary tree:
```
   1
    \
     3
    / \
   2   4
        \
         5
```
Longest consecutive sequence path is 3-4-5, so return 3.
```
   2
    \
     3
    / 
   2    
  / 
 1
 ```
 Longest consecutive sequence path is 2-3,not3-2-1, so return 2.

- Solution 1: Traverse
```java
public class Solution {
    private int result = 1;
    public int longestConsecutive(TreeNode root) {
        // write your code here
        traverse(root, null, 1);
        return result;
    }
    
    private void traverse(TreeNode current, TreeNode prev, int path) {
        if (current == null) {
            return ;
        }
        
        if (prev != null && (prev.val + 1 == current.val)) {
            path ++;
            result = Math.max(result, path);
        } else {
            path = 1;
        }
        
        traverse(current.left, current, path);
        traverse(current.right, current, path);
    }
    
}
```    
