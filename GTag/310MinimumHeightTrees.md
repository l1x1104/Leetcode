[Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/description/)

```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        
        List<Integer> result = new ArrayList<>();
        if (n == 0 || edges == null) {
            return result;
        } else if (n == 1) {
            result.add(0);
            return result;
        }
        
        List<Integer>[] nodes = new ArrayList[n];
        for (int i = 0 ; i < n; i++) {
            nodes[i] = new ArrayList<>();
        }
        for (int i = 0 ; i < edges.length; i++) {
            int val1 = edges[i][0];
            int val2 = edges[i][1];
            nodes[val1].add(val2);
            nodes[val2].add(val1);
        }
        
        List<Integer> leaves = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            if (nodes[i].size() == 1) {
                leaves.add(i);
            }
        }
        
        int count = n;
        while (count > 2) {
            int size = leaves.size();
            count -= size;
            List<Integer> newLeaves = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                int leaf = leaves.get(i);
                int toRemove = nodes[leaf].get(0);
                nodes[leaf] = null;
                List<Integer> tmpList = nodes[toRemove];
                tmpList.remove(tmpList.indexOf(leaf));
            }
            
            for (int j = 0; j < n; j++) {
                if (nodes[j] != null && (nodes[j].size() == 1 || nodes[j].size() == 0)) {
                    newLeaves.add(j);
                }
            }
            
            leaves = newLeaves;
        }
        
        return leaves;
    }
}
```
