[二叉树垂直遍历](https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/)

```java
class Solution {
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        Queue<TreeNode> qNode = new LinkedList<>();
        Queue<Integer> qIdx = new LinkedList<>();
        Map<Integer, List<Integer>> map = new HashMap<>();
        
        int min = 0, max = 0;
        TreeNode curr = root;
        qNode.offer(curr);
        qIdx.offer(0);
        while (!qNode.isEmpty()) {
            int size = qNode.size();
            for (int t = 0; t < size; t++) {
                curr = qNode.poll();
                int num = qIdx.poll();
                
                min = Math.min(min, num);
                max = Math.max(max, num);
                
                if (map.containsKey(num)) {
                    map.get(num).add(curr.val);
                } else {
                    List<Integer> tmpList = new ArrayList<>();
                    tmpList.add(curr.val);
                    map.put(num, tmpList);
                }
                
                if (curr.left != null) {
                    qNode.offer(curr.left);
                    qIdx.offer(num - 1);
                }
                if (curr.right != null) {
                    qNode.offer(curr.right);
                    qIdx.offer(num + 1);
                }
            }          
        }
        
        for (int i = min; i <= max; i++) {
            result.add(map.get(i));
        }
        
        return result;
    }
}
```
