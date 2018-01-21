* Solution 1 Iterative(using Queue)
```java
public class Solution {
    public void connect(TreeLinkNode root) {
        // level order traversal
        if (root == null) return ;
        
        Queue<TreeLinkNode> q = new LinkedList<>();
        q.offer(root);
        while (!q.isEmpty()) {
            int size = q.size();
            TreeLinkNode prev = null;
            for (int i = 0; i < size; i++) {
                TreeLinkNode curr = q.poll();
                if (size == 1) {
                    curr.next = null;
                } 
                if (prev != null) {
                    prev.next = curr;
                }
                if (curr.left != null) q.offer(curr.left);
                if (curr.right != null) q.offer(curr.right);
                prev = curr;
            }       
        }
    }
}
```
```java
public void connect(TreeLinkNode root) {
    if(root == null)
        return;
        
    if(root.left != null){
        root.left.next = root.right;
        if(root.next != null)
            root.right.next = root.next.left;
    }
    
    connect(root.left);
    connect(root.right);
}
```
