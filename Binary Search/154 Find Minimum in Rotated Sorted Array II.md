- - -
Follow up for "Find Minimum in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates.

```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0, r = nums.length - 1;   
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] < nums[r]) {
                r = mid;
            } else if (nums[mid] > nums[r]) {
                l = mid + 1;
            } else {
                r --;
            }
        }
        return nums[l];
    }
}
```

### 这题只有边界的重复问题要考虑<br> 
不能像I那样粗暴地 r = mid; (万一夹在两者之中呢？)随便举一个例子，nums[mid]等于nums[r],而最小值在右区间，你的操作是,r = mid, 比如[4,4,4,4,2,3,4].
              
这样写也对.注意 nums[mid]与nums[r]相等，要又指针向左移("r--")，因为你要求的是最小值，偏左.

```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0, r = nums.length - 1;   
        while (l < r) {
            int mid = l + ((r - l) >> 1);
            if (nums[mid] < nums[r]) {
                r = mid;
            } else if (nums[mid] > nums[r]) {
                l = mid + 1;
            } else {
                r --;
            }
        }
        return nums[r];
    }
}
```

