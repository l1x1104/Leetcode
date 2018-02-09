[Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0 || nums.length == 1 && target != nums[0]) {
            return -1;
        }
        
        int left = 0, right = nums.length - 1;
        while (left + 1 <  right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[left] < nums[mid]) {
                if (nums[left] <= target && target <= nums[mid]) {
                    right = mid;
                } else {
                    left = mid;
                }
            }
            
            if (nums[mid] < nums[right]) {
                if (nums[mid] <= target && target <= nums[right]) {
                    left = mid;
                } else {
                    right = mid;
                }
            }
            
        }
        
        if (nums[left] == target) {
            return left;
        } else if (nums[right] == target) {
            return right;
        }
        
        return -1;
    }
}
```
