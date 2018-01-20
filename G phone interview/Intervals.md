***
#### 给一堆区间，比如 [-1.1, 1.0], [-0.5, 3.5], [3.6, 4.0], ..., 再给一个点target，比如0.1，要返回所有包含了这个点的区间<br>
最简单的做法就是一个一个区间比较, 返回所有包含了target的区间，这是linear time. <br>
可以对这些区间做pre-processing, pre-processing只做一次所以复杂度不计。问怎么做可以比linear time更快. <br>
大致思路是，按照区间左端点做sorting，然后binary search.

        
input: [1,2][2,6][3,4][5,8][6,7] target = 5 <br>
Expected: [2,6][5,8] <br>
start: 1, 2, 3, 5, 6 <br>
end:   2, 4, 6, 7, 8 <br>

1: [1,2]       1            2 <br>
2: [2,6]       1 + 1 - 1    4 <br>
3: [2,6][3,4]  1 + 1        4 <br>
5: [2,6][5,8]  2 + 1 - 1    6 <br>
6: [5,8][6,7]  2 + 1 - 1    7 <br>
- 你需要记录在每一个start point(以这个start作为target)对应的list, 这是预处理. 用bs找target对应的list，这是search，用时logN. 面试官要求优化这部分.

##### 最巧妙的地方如果遇到“-1”，如果知道删掉哪几个？
- 我把这个问题分成了“删掉几个？”+“删掉最小的X个因为他们最快过期）”. 删掉几个很好解决，去掉负号即可. 最小的？-> minHeap.

```java
private List<Interval> findIntervals(double target, Interval[] intervals) {
    if (intervals == null || intervals.length == 0) {
        return null;
    }
    // find max value and use it as new length of start & end
    int n = Integer.MIN_VALUE;
    for (int i = 0; i < intervals; i++) {
        n = Math.max(n, intervals[i].end);
    }
    
    int[] start = new int[n + 1];
    int[] end = new int[n + 1];
    
    for (int i = 0; i < intervals.length; i++) {
        start[intervals[i].start] ++;
        end[intervals[i].end] --;
    }
    
    // Have to sort, so
    Arrays.sort(intervals, new Comparator<Interval>() {
        public int compare(Interval a, Interval b) { return a.start - b.start; }
    });
    
    // use minHeap to record at a specific point how many intervals still include this point
    // (so you can use binary search next step)
    PriorityQueue<Interval> tempList = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>() {
        public int compare(Interval a, Integerval b) {
            return a.end - b.end;
        }
    });
    
    // Stretch all points(including start & end) to a line on x coordinate
    List<List<Interval>> res = new ArrayList<>();
    int index = 0; // to index start point so that we know which interval to be added to tempList
    
    for (int t = 0; t < n + 1; t++) {
        if (start[t] != 0) { // means there must be interval start as this value
            int len  = start[t];
            for (int i = 0; i < len; i++) {
                tempList.offer(intervals[index++]);
            }
        }
        if (end[t] != 0) {
            int len = - end[t];
            for (int j = 0; j < len; j++) {
                tempList.poll();
            }
        }
        res.add(new ArrayList<>(tempList)); // So res is 
    }
    
    // Binary Search
    indexOfTarget = binarySearch(res, target);
    List<Interval> result = res.get(target);
    return result;
}
private int binarySearch(Interval[] intervals, int target) {   // Binary Search格式不改了，就意思一下
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
