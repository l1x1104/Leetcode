[总结区间](https://leetcode.com/problems/summary-ranges/description/)

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> result = new ArrayList<>();
        
        int n = nums.length, i = 0;
        while (i < n) {
            int j = 1;
            while (i + j < n && nums[i + j] - nums[i] == j) {
                j ++;
            }
            String str = j == 1 ? Integer.toString(nums[i]) : Integer.toString(nums[i]) + "->" + Integer.toString(nums[i + j - 1]);
            result.add(str);
            i += j;
        }
        
        return result;
    }
}
```
