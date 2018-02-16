[整平二维向量](https://leetcode.com/problems/flatten-2d-vector/description/)

```java
public class Vector2D implements Iterator<Integer> {
    Queue<Integer> q = new LinkedList<>();
    public Vector2D(List<List<Integer>> vec2d) {
        for (List<Integer> list: vec2d) {
            for (Integer num: list) {
                q.offer(num);
            }
        }
    }

    @Override
    public Integer next() {
        if (hasNext()) {
            return q.poll();
        } else {
            return Integer.MAX_VALUE;
        }
    }

    @Override
    public boolean hasNext() {
        return q.size() > 0;
    }
}
```
