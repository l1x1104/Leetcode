[求除法表达式的值](https://leetcode.com/problems/evaluate-division/description/)

```java
class Solution {
    public double[] calcEquation(String[][] equations, double[] values, String[][] queries) {
        double[] res = new double[queries.length];
        HashMap<String, HashMap<String, Double>> map = new HashMap<>();
        
        for (int i = 0; i < equations.length; ++i) {
            if (!map.containsKey(equations[i][0])) {
                map.put(equations[i][0], new HashMap<String, Double>());
            }
            if (!map.containsKey(equations[i][1])) {
                map.put(equations[i][1], new HashMap<String, Double>());
            }
            map.get(equations[i][0]).put(equations[i][1], values[i]);
            map.get(equations[i][1]).put(equations[i][0], 1.0 / values[i]);
        }
        
        double[] result = new double[queries.length];
        for (int i = 0; i < queries.length; ++i) {
            if (map.containsKey(queries[i][0]) && map.containsKey(queries[i][1])) {
                if (queries[i][0] == queries[i][1]) {
                    // "a", "a"
                    result[i] = 1.0;
                } else {
                    double tmp = dfs(queries[i][0], queries[i][1], new HashSet<String>(), map, 1.0);
                    result[i] = tmp == 0.0 ? -1.0 : tmp;
                }
            } else {
                //"a", "e", "x", "x"
                result[i] = -1.0;
            }
        }
        return result;
    }
    
    private double dfs(String s, String t, HashSet<String> visited, HashMap<String, HashMap<String, Double>> map, double val) {
        if (map.get(s).containsKey(t)) {
            return val * map.get(s).get(t);
        }
        
        double tmp = 0.0;
        for (String neighbor : map.get(s).keySet()) {
            if (!visited.contains(neighbor)) {
                visited.add(neighbor);
                tmp = dfs(neighbor, t, visited, map, val * map.get(s).get(neighbor));
                if (tmp != 0.0) break;
            }
        }
        
        return tmp;    
    }
}
```
