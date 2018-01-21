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
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        int count = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            while (size > 0) {
                TreeNode curr = q.poll();
                if (curr.left != null) {
                    q.offer(curr.left);
                }
                if (curr.right != null) {
                    q.offer(curr.right);
                }
                size --;
            }
            count ++;
        }
        return count;
    }
}
```

***
* 最短路径？难点在于，末节点返回值和普通节点左/右节点返回值要区分开来.
```java
class Solution {
    public int minDepth(TreeNode root) {
        if(root == null) return 0;
        
        if(root.left == null && root.right == null) {
            return 1;
        } else if(root.left == null || root.right == null) {
            if(root.left != null) return 1 + minDepth(root.left);
            if(root.right != null) return 1 + minDepth(root.right);
        }
        
        return 1 + Math.min(minDepth(root.left), minDepth(root.right));
    }
}
```
上面iterative的方法改了一下
```java
class Solution {
    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        
        Stack<TreeNode> st = new Stack<>();
        Stack<Integer> sv = new Stack<>();
        st.push(root);
        sv.push(1);
        int min = Integer.MAX_VALUE;
    
        while (!st.isEmpty()) {
            TreeNode curr = st.pop();
            int temp = sv.pop();
            if (curr.left == null && curr.right == null) min = Math.min(temp, min);
            if (curr.left != null) {
                st.push(curr.left);
                sv.push(temp + 1);
            }
            if (curr.right != null) {
                st.push(curr.right);
                sv.push(temp + 1);
            }       
        }
        return min == Integer.MAX_VALUE? 1 : min;
    }
}
```
