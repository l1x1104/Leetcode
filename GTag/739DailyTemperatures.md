[日常温度](https://leetcode.com/problems/daily-temperatures/description/)

递减栈Descending stack
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int t = stack.pop();
                result[t] = i - t;
            }
            stack.push(i);
        }
        
        return result;
    }
}
```
