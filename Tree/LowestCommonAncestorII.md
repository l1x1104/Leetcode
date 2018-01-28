#### Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes. The lowest common ancestor is the node with largest depth which is the ancestor of both nodes. The node has an extra attribute parent which point to the father of itself. The root's parent is null.
- Example
- For the following binary tree:
```
  4
 / \
3   7
   / \
  5   6
LCA(3, 5) = 4
LCA(5, 6) = 7
LCA(6, 7) = 7  
```

* Solution 1: HashSet (Time: O(h) h is the height of the tree)
```java
/**
 * Definition of ParentTreeNode:
 * 
 * class ParentTreeNode {
 *     public ParentTreeNode parent, left, right;
 * }
 */

public class Solution {
    /*
     * @param root: The root of the tree
     * @param A: node in the tree
     * @param B: node in the tree
     * @return: The lowest common ancestor of A and B
     */
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root, ParentTreeNode A, ParentTreeNode B) {
        // write your code here
        HashSet<TreeNode> set = new HashSet<>();
        
        while (A != null || B != null) {
            if (A != null) {
                if (set.contains(A)) {
                    return A;
                }
                set.add(A);
                A = A.parent;
            }
            
            if (B != null) {
                if (set.contains(B)) {
                    return B;
                }
                set.add(B);
                B = B.parent;
            }
        }
        
        return null;
    }
}
```

