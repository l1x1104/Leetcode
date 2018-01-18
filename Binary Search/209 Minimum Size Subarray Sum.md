- - -
Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the 
sum ≥ s. If there isn't one, return 0 instead.

For example, given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.

### 方法：Two pointers：一个记录连续的开始，一个往前走直到连续区间尾。 consecutive可以连续减，也可连续加。
     
### 1 Two Pointers - O(n)
```java
class Solution {
    public int minSubArrayLen(int s, int[] a) {
        if (a == null || a.length == 0) return 0;
        int i = 0, j = 0, sum = 0, min = Integer.MAX_VALUE;
        while (j < a.length) 
            sum += a[j++];
            while (sum >= s) {
                min = Math.min(min, j - i);
                sum -= a[i++];
            }
        return min == Integer.MAX_VALUE ? 0 : min;
    }
}
```

### 2 Binary Search - O(nlogn)
```java
public class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        return solveNLogN(s, nums);
    }

    private int solveNLogN(int s, int[] nums) {
        int[] sums = new int[nums.length + 1];
        for (int i = 1; i < sums.length; i++) sums[i] = sums[i - 1] + nums[i - 1];
            int minLen = Integer.MAX_VALUE;
            for (int i = 0; i < sums.length; i++) {
               int end = binarySearch(i + 1, sums.length - 1, sums[i] + s, sums);
               if (end == sums.length) break;
               if (end - i < minLen) minLen = end - i;
            }
        return minLen == Integer.MAX_VALUE ? 0 : minLen;
    }
    
    private int binarySearch(int lo, int hi, int key, int[] sums) {
        while (lo <= hi) {
           int mid = (lo + hi) / 2;
           if (sums[mid] >= key){
               hi = mid - 1;
           } else {
               lo = mid + 1;
           }
        }
        return lo;
    }
 }
```
- - -
## 骚操作 - 如何快速找到sum >= s的连续区间？
### 给一个数组(不一定有序), [2,3,1,2,4,3] s = 7. 
肉眼找大于7的连续区间 [4,3], [1,2,4], [2,4,3], [2,3,1,2],[3,1,2,4],[1,2,4,3]...(后面几个太长了..不重要跳过..)

### 新建一个数组 nums, 长度比原数组大1.
index 0 1 2 3 4 5  6 <br>
     [2,3,1,2,4,3] <br>
     [0,2,5,6,8,12,15] <br>
     
     从index = i开始连续几个数以后大于7？ 用bs在新数组nums里面找target(target == (nums[index] + s)). 比如i = 0, target = 7. <br>
     i = 3, target = 13, index = 6 . i = 4, target = 15, index = 6. 从原数组中可以看到index 3~5 和 4~5和都大于等于7.
     程序实现如下: 
     
     ```java
     for (int z = 0; z < cache.length; z++) {
            int index = binarySearch(z + 1, cache[z] + s, cache);
            //System.out.println(" return index: " + index);
            if (index == cache.length) break;
            else {
                len = Math.min(index - z, len);
                //System.out.println(" start: " + z + ", target : " + (cache[z] + s) + ", len:" + len);
                //System.out.println("--------");
            }
        } 
     ```
