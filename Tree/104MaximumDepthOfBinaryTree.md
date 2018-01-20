***
* 最长路径，一般没有大问题
```java
略
```
##### This is the iterative version of finding the depth. The recursive version is trivial, so expect the interviewer to ask for the iterative version. I used two stacks for the dfs one and a queue for the level-order traversal one. Level order one is faster.
* DFS
```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        Stack<TreeNode> st = new Stack<>();
        Stack<Integer> sv = new Stack<>();
        st.push(root);
        sv.push(1);
        int max = 0;
    
        while (!st.isEmpty()) {
            TreeNode curr = st.pop();
            int temp = sv.pop();
            max = Math.max(temp, max);
            if (curr.left != null) {
                st.push(curr.left);
                sv.push(temp + 1);
            }
            if (curr.right != null) {
                st.push(curr.right);
                sv.push(temp + 1);
            }       
        }
        return max;
    }
}
```
* BFS
```java
public int maxDepth(TreeNode root) {
    if(root == null) {
        return 0;
    }
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    int count = 0;
    while(!queue.isEmpty()) {
        int size = queue.size();
        while(size-- > 0) {
            TreeNode node = queue.poll();
            if(node.left != null) {
                queue.offer(node.left);
            }
            if(node.right != null) {
                queue.offer(node.right);
            }
        }
        count++;
    }
    return count;
}
```
