[Max Chunks To Make Sorted](https://leetcode.com/problems/max-chunks-to-make-sorted/description/)

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
