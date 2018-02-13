[我的日历之二](https://leetcode.com/problems/my-calendar-ii/description/)

```java
class MyCalendarTwo {
    private List<int[]> books;
    private List<int[]> overlaps;
    
    public MyCalendarTwo() {
        books = new ArrayList<>();
        overlaps = new ArrayList<>();    
    }
    
    public boolean book(int start, int end) {
    for (int[] overlap : overlaps) {
        if (Math.max(overlap[0], start) < Math.min(overlap[1], end)) {
            return false;
        }
    }
    for (int[] book : books) {
        int overlapStart = Math.max(book[0], start);
        int overlapEnd = Math.min(book[1], end);
        if (overlapStart < overlapEnd) {
            overlaps.add(new int[]{overlapStart, overlapEnd});
        }
    }
        
    books.add(new int[]{start, end});
        
    return true;        
    }
}
```

```java
class MyCalendarTwo {
    private List<int[]> bookings;
    private List<int[]> overlaps;
    
    public MyCalendarTwo() {
        bookings = new ArrayList<>();
        overlaps = new ArrayList<>();
    }
    
    public boolean book(int start, int end) {
        for (int[] bo: bookings) {
            int overlapStart = Math.max(bo[0], start), overlapEnd = Math.min(bo[1], end);
            if (overlapStart < overlapEnd) {
                for (int[] ov: overlaps) {
                    if (Math.max(ov[0], overlapStart) < Math.min(ov[1], overlapEnd)) {
                        overlaps.clear();
                        return false;
                    }
                }
                overlaps.add(new int[] {overlapStart, overlapEnd});
            }
        } 
        bookings.add(new int[] {start, end});
        return true;
    }
}
```
