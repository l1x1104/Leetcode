***
#### Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST. Calling next() will return the next smallest number in the BST. Note: next() and hasNext() should run in average O(1) time and uses O(h) memory, where h is the height of the tree.

* Solution 1 - Stack
```java
public class BSTIterator {

    Stack<TreeNode> stack = new Stack<TreeNode> ();
    
    public BSTIterator(TreeNode root) {
        while (root != null) {
           stack.push(root);
           root = root.left;
        }
    }

    /** @return whether we have a next smallest number */
    public boolean hasNext() {
        return !stack.isEmpty();
    }

    /** @return the next smallest number */
    public int next() {
        TreeNode tmp = stack.pop();
        TreeNode runner = tmp.right;
        while (runner != null) {
            stack.push(runner);
            runner = runner.left;
        }
        return tmp.val;
    }
}
```

* Solution 2 - Two Pointers(Morris Traversal)
```java
public class BSTIterator {
	  private TreeNode curr;
    
    public BSTIterator(TreeNode root) {
		TreeNode prev;
		curr = root;
		while(curr != null){
			if(curr.left == null){
				curr = curr.right;
			}
			else{
				prev = curr.left;
				while(prev.right != null && prev.right != curr)
					prev = prev.right;

				if(prev.right == null){
					prev.right = curr;
					curr = curr.left;
				}
				else{
					curr = curr.right;
				}
			}
		}
		curr = root;
		while(curr != null && curr.left != null)
			  curr = curr.left;
    }

    public boolean hasNext() {
		    return curr != null;
    }

    public int next() {
		int result = curr.val;
		TreeNode next = curr.right;
		if(next == null)
			curr = next;
		else if(next.left == null || next.left.val > curr.val){
			curr = next;
			while(curr.left != null)
				curr = curr.left;
		} else {
			curr.right = null;//we recover the original tree structure
			curr = next;
		}

		return result;
    }
}
```
