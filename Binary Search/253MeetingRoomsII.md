***
#### Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.
* For example
- Given [[0, 30],[5, 10],[15, 20]],
- return 2

##### Solution 1 - Two arrays
任何一个会议室结束时间小于任意一个会议室开始时间意味着 一定有一个会议结束，会议室能空出来
```java
public class Solution {
    public int minMeetingRooms(Interval[] intervals) {
        int[] starts = new int[intervals.length];
        int[] ends = new int[intervals.length];
        for(int i=0; i<intervals.length; i++) {
            starts[i] = intervals[i].start;
            ends[i] = intervals[i].end;
        }
        Arrays.sort(starts);
        Arrays.sort(ends);
        int rooms = 0;
        int endsItr = 0;
        for(int i=0; i<starts.length; i++) {
            if(starts[i]<ends[endsItr])
                rooms++;
            else
                endsItr++;
        }
        return rooms;
    }
} 
```

##### Solution 2 - Priority Queue
```java
public int minMeetingRooms(Interval[] intervals) {
    if (intervals == null || intervals.length == 0)
        return 0;
        
    // Sort the intervals by start time
    Arrays.sort(intervals, new Comparator<Interval>() {
        public int compare(Interval a, Interval b) { 
            return a.start - b.start; 
        }
    });
    
    // Use a min heap to track the minimum end time of merged intervals
    PriorityQueue<Interval> pq = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>() {
        public int compare(Interval a, Interval b) { 
            return a.end - b.end; 
        }
    });
    
    // start with the first meeting, put it to a meeting room
    pq.offer(intervals[0]);
    
    for (int i = 1; i < intervals.length; i++) {
        // get the meeting room that finishes earliest
        Interval interval = pq.poll();
        
        if (intervals[i].start >= interval.end) {
            // if the current meeting starts right after 
            // there's no need for a new room, merge the interval
            interval.end = intervals[i].end;
        } else {
            // otherwise, this meeting needs a new room
            pq.offer(intervals[i]);
        }
        
        // don't forget to put the meeting room back
        pq.offer(interval);
    }
    
    return pq.size();
}
```

##### Solution 3 - O(n) 
If we draw a vertical line in time point, "-1" when meet the begin point, "+1" when meet the end point.
Traverse and record the maximum number.
```java
    public int minMeetingRooms(Interval[] intervals) {
        if (intervals == null || intervals.length == 0) {
            return 0;
        }
        
        Arrays.sort(intervals, new Comparator<Interval>() {
            public int compare(Interval a, Interval b) { 
                return a.start - b.start; 
            }
        });
        PriorityQueue<Interval> pq = new PriorityQueue<Interval>(intervals.length, new Comparator<Interval>() {
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
```
```java
    public int minMeetingRooms(Interval[] intervals) {
        if(intervals.length == 0) return 0;
        int maxtime = Integer.MIN_VALUE;
        //Find max meeting time
        for(int i = 0; i < intervals.length; i++){
            maxtime = Math.max(maxtime, intervals[i].end);
        }
        int[] cont = new int[maxtime+1];
        for(int i = 0; i < intervals.length; i++){
            cont[intervals[i].start]++;
            cont[intervals[i].end]--;
        }
        int res = 0;
        for(int i = 1; i <= maxtime; i++){
            cont[i] += cont[i-1];
            res = Math.max(res, cont[i]);
        }
        return res;
    }
```
