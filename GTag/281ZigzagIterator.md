[Z形迭代器](https://leetcode.com/problems/zigzag-iterator/description/)
```
Given two 1d vectors, implement an iterator to return their elements alternately.

For example, given two 1d vectors:

v1 = [1, 2]
v2 = [3, 4, 5, 6]
By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1, 3, 2, 4, 5, 6].

Follow up: What if you are given k 1d vectors? How well can your code be extended to such cases?

Clarification for the follow up question - Update (2015-09-18):
The "Zigzag" order is not clearly defined and is ambiguous for k > 2 cases. If "Zigzag" does not look right to you, replace "Zigzag" with "Cyclic". For example, given the following input:

[1,2,3]
[4,5,6,7]
[8,9]
It should return [1,4,8,2,5,9,3,6,7].

```

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
```java
public class ZigzagIterator {
    Iterator<Integer> cur_iterator;
    Iterator<Integer> iterator1;
    Iterator<Integer> iterator2;
    
    public ZigzagIterator(List<Integer> v1, List<Integer> v2) {
        this.iterator1 = v1.iterator();
        this.iterator2 = v2.iterator();
        this.cur_iterator = (this.iterator1.hasNext() ? this.iterator1 : this.iterator2);
    }

    public int next() {
        int ret = cur_iterator.next();
        if (cur_iterator == iterator1) {
            if (iterator2.hasNext()) {
                cur_iterator = iterator2;
            }
        } else{
            if (iterator1.hasNext()) {
                cur_iterator = iterator1;
            }
        }
        return ret;
    }

    public boolean hasNext() {
        return cur_iterator.hasNext();
    }
}
```
