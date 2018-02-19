[合并区间](https://leetcode.com/problems/merge-intervals/description/)

```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> result = new ArrayList<>();
        
        intervals.sort(Comparator.comparing(i -> i.start));
        /*Collection.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval a, Interval b) {
                return a.start - b.start;
            }
        }); */
        
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
