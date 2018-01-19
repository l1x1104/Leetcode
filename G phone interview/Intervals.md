***
#### 给一堆区间，比如 [-1.1, 1.0], [-0.5, 3.5], [3.6, 4.0], ..., 再给一个点target，比如0.1，要返回所有包含了这个点的区间<br>
最简单的做法就是一个一个区间比较, 返回所有包含了target的区间，这是linear time. <br>
可以对这些区间做pre-processing, pre-processing只做一次所以复杂度不计。问怎么做可以比linear time更快. <br>
大致思路是，按照区间左端点做sorting，然后binary search.

        
input: [1,2][2,6][3,4][5,8][6,7] target = 5 <br>
Expected: [2,6][5,8] <br>
start: 1, 2, 3, 5, 6 <br>
end:   2, 4, 5, 7, 8 <br>

1: [1,2]       1            2
2: [2,6]       1 + 1 - 1    4
3: [2,6][3,4]  1 + 1        4
5: [2,6][5,8]  2 + 1 - 1    5
6: [5,8][6,7]  2 + 1 - 1    7

```java
private Interval findIntervals(double target, Interval[] intervals) {
    if (intervals == null || intervals.length == 0) {
        return null;
    }
    
    PriorityQueue<Interval> pq = new PriorityQueue<Interval>(new Comparator<Interval>() {
        public int compare(Interval a, Integerval b) {
            return a.end - b.end;
        }
    });
    for (Interval i: intervals) {
        pq.offer(i);
    }
    
    Arrays.sort(intervals, new Comparator<Interval>() {
        public int compare(Interval a, Interval b) {
            return a.start - b.start;
        }
    });
    
    List<Interval> res = new ArrayList<>();
    for (int t = 0; t < intervals.length; t++) {
        res.add(intervals[t]);
        Interval curr = pq.peek();
        if (intervals[t].start >= curr.end) {
                          
        }
    }
    
}
private int binarySearch(Interval[] intervals, int target) {
    int left = 0, right = intervals.length;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (intervals[mid].start < target) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
    return left;
}
```
