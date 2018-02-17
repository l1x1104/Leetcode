[下一个较大元素之二](https://leetcode.com/problems/next-greater-element-ii/description/)

- Solution 1: brute force
```java
public class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        Arrays.fill(result, -1);
        
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < i + n; j++) {
                if (nums[j % n] > nums[i]) {
                    result[i] = nums[j % n];
                    break;
                }
            }
        }
        
        return result;
    }
}
```

- Solution 2: stack
```java
public class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        Arrays.fill(result, -1);
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i < 2 * n; i++) {
            int num = nums[i % n];
            while (!stack.isEmpty() && nums[stack.peek()] < num) {
                result[stack.pop()] = num;
            }
            if (i < n) {
                stack.push(i);
            }
        }
        
        return result;
    }
}
```
