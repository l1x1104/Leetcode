#### Given the root and two nodes in a Binary Tree. Find the lowest common ancestor(LCA) of the two nodes. The lowest common ancestor is the node with largest depth which is the ancestor of both nodes.
Return null if LCA does not exist.
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
* Notice : <br>
node A or node B may not exist in tree.

* Solution 1: HashSet (Time: O(h) h is the height of the tree) <br>
对 p 和 q 向上走，用 hashtable 记录访问过的节点，如果某个节点已经被访问过了，那么返回该节点.
```java
