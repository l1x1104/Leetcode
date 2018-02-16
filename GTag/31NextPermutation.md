[下一个排列](https://leetcode.com/problems/next-permutation/description/)

interesting & simple once you know this algo
```java
class Solution {
    public void nextPermutation(int[] nums) {
        if (nums == null || nums.length == 0) {
            return;
        }
        
    	int k = -1;
    	for (int i = nums.length - 2; i >= 0; i--) {
    		if (nums[i] < nums[i + 1]) {
    			k = i;
    			break;
    		}
    	} 
        
    	if (k == -1) {
    	    Arrays.sort(nums);
    	    return;
    	}
        
    	int l = -1;
    	for (int i = nums.length - 1; i > k; i--) {
    		if (nums[i] > nums[k]) {
    			l = i;
    			break;
    		} 
    	} 
    	// swap
        int temp = nums[k];
        nums[k] = nums[l];
        nums[l] = temp;
        
    	Arrays.sort(nums, k + 1, nums.length);        
    }
}
```
