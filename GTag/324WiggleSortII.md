[摆动排序](https://leetcode.com/problems/wiggle-sort-ii/description/)

- Solution 1: Space O(n)
```java
class Solution {
    public void wiggleSort(int[] nums) {
        int n = nums.length;
        if (n == 0) return ;
        Arrays.sort(nums);
        
        int[] arr = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            arr[i] = nums[i];
        }
        
        int k = (n + 1) / 2, j = n;
        for (int i = 0; i < n; i++) {
            nums[i] = i % 2 == 0 ? arr[--k] : arr[--j];
        }        
    }
}
```

- FollowUp : Time O(n) Space O(1) <br>
"Virtual Indexing" - https://leetcode.com/problems/wiggle-sort-ii/discuss/77677/O(n)+O(1)-after-median-Virtual-Indexing

