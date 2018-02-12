[Z形迭代器](https://leetcode.com/problems/zigzag-iterator/description/)

```java
public class ZigzagIterator {
    private int i = 0;
    private List<Integer> list = new ArrayList<>();
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        int m = v1.size(), n = v2.size(), size = Math.max(m, n);
        for (int i = 0; i < size; i++) {
            if (i < m) list.add(v1.get(i));
            if (i < n) list.add(v2.get(i));
        }
    }

    public int next() {
        return list.get(i++);
    }

    public boolean hasNext() {
        return i < list.size();
    }
}

/**
 * Your ZigzagIterator object will be instantiated and called as such:
 * ZigzagIterator i = new ZigzagIterator(v1, v2);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

- FollowUp: K个数组怎么办
通解 <br>
Uses a linkedlist to store the iterators in different vectors. Every time we call next(), we pop an element from the list, and re-add it to the end to cycle through the lists.
```java
public class ZigzagIterator {
    LinkedList<Iterator> list;
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        list = new LinkedList<Iterator>();
        if(!v1.isEmpty()) list.add(v1.iterator());
        if(!v2.isEmpty()) list.add(v2.iterator());
    }

    public int next() {
        Iterator poll = list.remove();
        int result = (Integer)poll.next();
        if(poll.hasNext()) list.add(poll);
        return result;
    }

    public boolean hasNext() {
        return !list.isEmpty();
    }
}
```
