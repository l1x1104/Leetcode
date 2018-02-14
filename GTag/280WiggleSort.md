[摆动排序](https://leetcode.com/problems/wiggle-sort/description/)
```
Given an unsorted array nums, reorder it in-place such that nums[0] <= nums[1] >= nums[2] <= nums[3]....

For example, given nums = [3, 5, 2, 1, 6, 4], one possible answer is [1, 6, 2, 5, 3, 4].
```

- Time: O(nlogn)
```java
class Solution {
    public void wiggleSort(int[] nums) {
        int n = nums.length;
        if (n <= 2) {
            return ;
        }
        
        Arrays.sort(nums);

        for (int i = 2; i < n; i = i + 2) {
            int tmp = nums[i - 1];
            nums[i - 1] = nums[i];
            nums[i] = tmp;
        }
    }
    
}
```

- Time: O(n)
```java
class Solution {
    public void wiggleSort(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        if (n <= 1) {
            return ;
        }

        for (int i = 1; i < n; i ++) {
            if ((i % 2 == 1 && nums[i] < nums[i - 1]) || (i % 2 == 0 && nums[i] > nums[i - 1])) {
                int tmp = nums[i - 1];
                nums[i - 1] = nums[i];
                nums[i] = tmp;
            }
        }
    }    
}
```
