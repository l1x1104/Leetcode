[插入区间](https://leetcode.com/problems/insert-interval/description/)

```java
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> result = new ArrayList<>();
        int idx = 0;
        
        while (idx < intervals.size() && intervals.get(idx).start < newInterval.start) {
            idx++;
        }
        intervals.add(idx, newInterval);
        
        Interval last = null;
        for (Interval item: intervals) {
            if (last == null || item.start > last.end) {
                result.add(item);
                last = item;
            } else {
                last.end = Math.max(last.end, item.end);
            }
        }
        
        return result;
    }
}
```
