[下一个较大的元素之一](https://leetcode.com/problems/next-greater-element-i/description/)

- Solution 1: brute force (略)

- Solution 2: Map
```java
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        
        int[] result = new int[findNums.length];
        for (int i = 0; i < findNums.length; i++) {
            int index = map.get(findNums[i]);
            result[i] = -1;
            for (int j = index + 1; j < nums.length; j++) {
                if (nums[j] > findNums[i]) {
                    result[i] = nums[j];
                    break;
                }
            }
        }
        
        return result;
    }
}
```

- Solution 3: Map 和 Stack <br>
stack储存所有递减序列,举例 <br>
[4,2] <br>
[4,1,2,7] <br>
只要出现递增，递增(或群体递增比如4，2和7)就会和当前Number匹配放入map当中,否则存入stack当中.
```java
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Stack<Integer> s = new Stack<>();
        Map<Integer, Integer> mp = new HashMap<>();
        for(int num : nums) {
            while(!s.isEmpty() && s.peek() < num) {
                mp.put(s.pop(), num);
            }
            s.push(num);
        }
        for(int i = 0; i < findNums.length; i++) {
            findNums[i] = mp.getOrDefault(findNums[i], -1);
        }
        return findNums;
    }
}
```
