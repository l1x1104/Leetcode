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
Solution 2 - Recursive(preorder)
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
Solution 3  这个不用额外空间(Queue/Stack)的Level Order Traversal好厉害
```java
public class Solution {
    public void connect(TreeLinkNode root) {
        // Level Order Traversal
        TreeLinkNode head = null; //head of the next level
        TreeLinkNode prev = null; //the leading node on the next level
        TreeLinkNode cur = root;  //current node of current level

        while (cur != null) {   
            while (cur != null) { //iterate on the current level
                //left child
                if (cur.left != null) {
                    if (prev != null) {
                        prev.next = cur.left;
                    } else {
                        head = cur.left;
                    }
                    prev = cur.left;
                }
                //right child
                if (cur.right != null) {
                    if (prev != null) {
                        prev.next = cur.right;
                    } else {
                        head = cur.right;
                    }
                    prev = cur.right;
                }
                //move to next node
                cur = cur.next;
            }
            
            //move to next level
            cur = head;
            head = null;
            prev = null;
        }
    }
}
```
