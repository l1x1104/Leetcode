#### Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes. The lowest common ancestor is the node with largest depth which is the ancestor of both nodes. The node has an extra attribute parent which point to the father of itself. The root's parent is null.
* Example
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

* Solution 1: HashSet (Time: O(h) h is the height of the tree) <br>
对 p 和 q 向上走，用 hashtable 记录访问过的节点，如果某个节点已经被访问过了，那么返回该节点.
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

* Solution 2  <br>
高度比较高的向上移动，直到两个节点相遇。
```java
public class Solution {
    public ParentTreeNode lowestCommonAncestorII(ParentTreeNode root, ParentTreeNode A, ParentTreeNode B) {
        // write your code here
        int h1 = getHeight(A);
        int h2 = getHeight(B);
        
        // B is always deeper than A 
        if (h1 > h2) {  
            // swapNode
            ParentTreeNode tmp = A;
            A = B;
            B = tmp;
            
            // swapHeight
            int temp = h1;
            h1 = h2;
            h2 = temp; 
        }
        
        int dh = h2 - h1;
        for (int i = 0; i < dh; i++) {
            B = B.parent;
        }
        
        while (A != null && B != null) {
            if (A == B) {
                return A;
            }
            A = A.parent;
            B = B.parent;
        }
        
        return null;
        
    }
    
    private int getHeight (ParentTreeNode node) {
        int height = 0;
        while (node != null) {
            height ++;
            node = node.parent;
        }
        return height;
    }   
}
```
