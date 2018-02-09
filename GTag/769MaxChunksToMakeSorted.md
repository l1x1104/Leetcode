[Max Chunks To Make Sorted](https://leetcode.com/problems/max-chunks-to-make-sorted/description/)

- Solution 1
```java
class Solution {
    public int maxChunksToSorted(int[] arr) {
        if (arr.length == 0) {
            return 0;
        }
        
        int count = 0, idx = 0, prev = arr[0];
        
        while (idx != arr.length) {
            for (int i = idx; i <= prev; i++) {
                if (arr[i] > prev) {
                    prev = arr[i];
                }
            }
            count ++;
            idx = ++prev;
        }
        
        return count;
    }
}
```

- Solution 2
```java
class Solution {
    public int maxChunksToSorted(int[] arr) {
        if (arr.length == 0 || arr == null) {
            return 0;
        }
        
        int count = 0, max = 0;
        for (int t = 0; t < arr.length; t++) {
            max = Math.max(max, arr[t]);
            if (max == t) {
                count ++;
            }
        }
        
        return count;
    }
}
```
