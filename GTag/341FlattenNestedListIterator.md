[压平嵌套链表迭代器](https://leetcode.com/problems/flatten-nested-list-iterator/description/)

```java
public class NestedIterator implements Iterator<Integer> {
    private Stack<NestedInteger> stack = new Stack<>();
    public NestedIterator(List<NestedInteger> nestedList) {
        for (int i = nestedList.size() - 1; i >= 0; i--) {
            stack.push(nestedList.get(i));
        }
    }

    @Override
    public Integer next() {
        return stack.pop().getInteger();
    }

    @Override
    public boolean hasNext() {
        while (!stack.isEmpty()) {
            NestedInteger curr = stack.peek();
            if (curr.isInteger()) {
                return true;
            } 
            stack.pop();
            List<NestedInteger> list = curr.getList();
            for (int j = list.size() - 1; j >= 0; j--) {
                stack.push(list.get(j));
            }
        }
        return false;
    }
}
```
