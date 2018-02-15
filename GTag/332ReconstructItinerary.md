[重建行程单](https://leetcode.com/problems/reconstruct-itinerary/description/)

```java
public class Solution {  
    public List<String> findItinerary(String[][] tickets) {
        List<String> result = new ArrayList<>();
        if (tickets == null || tickets.length == 0 || tickets[0].length == 0) {
            return result;
        }
        
        Map<String, List<String>> map = new HashMap<>();
        // build graph
        for (int i = 0; i < tickets.length; i++) {
            String key = tickets[i][0];
            String val = tickets[i][1];
            if (!map.containsKey(key)) {
                map.put(key, new ArrayList<>());
            }
            map.get(key).add(val);
        }
        
        // sort adjList
        for (Map.Entry<String, List<String>> entry : map.entrySet()) {
            Collections.sort(entry.getValue());
        }
        
        result.add("JFK");
        dfs(map, result, "JFK", tickets.length + 1);
        
        return result;
    }
    private void dfs(Map<String, List<String>> map, List<String> result, String target, int n) {
        if (!map.containsKey(target)) {
            return ;
        }
        List<String> tmpList = map.get(target);
        for (int i = 0; i < tmpList.size(); i++) {
            String neighboor = tmpList.get(i);
            tmpList.remove(tmpList.indexOf(neighboor));
            result.add(neighboor);
            dfs(map, result, neighboor, n);
            if (result.size() == n) {
                return ;
            }
            tmpList.add(i, neighboor);
            result.remove(result.size() - 1);
        }       
    }
}
```
