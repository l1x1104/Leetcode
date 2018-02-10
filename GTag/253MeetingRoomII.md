[会议室II](https://leetcode.com/problems/meeting-rooms-ii/description/)

```java
class Solution {
    public int minMeetingRooms(Interval[] intervals) {
        if (intervals == null || intervals.length == 0) {
            return 0;
        }
        
        Arrays.sort(intervals, new Comparator<Interval>() {
            @Override
            public int compare(Interval a, Interval b) { 
                return a.start - b.start; 
            }
        });
        
        PriorityQueue<Interval> pq = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>() {
            @Override
            public int compare(Interval a, Interval b) { 
                return a.end - b.end; 
            }
        });
        
        for(Interval i: intervals) {
            pq.offer(i);
        }
        
        int rooms = 0, max = Integer.MIN_VALUE;
        for (int t = 0; t < intervals.length; t++) {
            Interval curr = pq.peek();
            rooms ++;
            if (intervals[t].start < curr.end) {
                max = Math.max(rooms, max);
            } else {
                rooms --;
                pq.poll();
            }
        }
        
        return max;     
    }
}
```
