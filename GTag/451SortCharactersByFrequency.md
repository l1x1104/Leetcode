[根据字符出现频率排序](https://leetcode.com/problems/sort-characters-by-frequency/description/)

- Solution 1: Bucket Sort
```java
class Solution {
   
    public String frequencySort(String s) {
        int n = s.length();
        char[] ch = s.toCharArray();
        int[] count = new int[130];
        
        for (int i = 0; i < n; i++) {
            count[ch[i]]++;
        }
        
        List<Character> [] arr = new List[n + 1];
        for (int j = 0; j < count.length; j++) {
            if (count[j] != 0) {
                if (arr[count[j]] == null) {
                    arr[count[j]] = new ArrayList<>();
                }
                char c = (char) j;
                arr[count[j]].add(c);
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for (int k = arr.length - 1; k >= 0; k--) {
            if (arr[k] != null) {
                List<Character> temp = arr[k];
                for (int l = 0; l < temp.size(); l++) {
                    for (int t = 0; t < k; t++) {
                        sb.append(temp.get(l));
                    }
                }
            }
        }
        
        return sb.toString();
        
    }
}
```

- Solution 2: PriorityQueue
```java
public String frequencySort(String s) {
        Map<Character, Integer> map = new HashMap<>();
        for (char c : s.toCharArray()) {
            if (map.containsKey(c)) {
                map.put(c, map.get(c) + 1);
            } else {
                map.put(c, 1);
            }
        }
        PriorityQueue<Map.Entry> pq = new PriorityQueue<>(map.size(), new Comparator<Map.Entry>() {
            @Override
            public int compare(Map.Entry o1, Map.Entry o2) {
                return (Integer) o2.getValue() - (Integer) o1.getValue();
            }
        });
        
        for (Map.Entry entry : map.entrySet()) {
            pq.offer(entry);
        }
        
        StringBuilder sb = new StringBuilder();
        while (!pq.isEmpty()) {
            Map.Entry entry = pq.poll();
            Character c = (Character) entry.getKey();
            Integer i = (Integer) entry.getValue();
            for (; i > 0; --i) {
                sb.append(c);
            }
        }
        return sb.toString();
    }
```
