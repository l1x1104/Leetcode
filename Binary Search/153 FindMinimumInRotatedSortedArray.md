- - -
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate exists in the array.

```java
class Solution {
    public int findMin(int[] nums) {
        int start = 0,  end = nums.length - 1;
        while (start < end) {
            if (nums[start] < nums[end]) {
                return nums[start];
            }
            int mid = start + (end - start) / 2;
            if (nums[mid] < nums[end]) {
                end = mid;
            } else {
                start = mid + 1;
            }
        }
        return nums[start];
    }
}
```


### 这题容易错的地方:
if (nums[mid] < nums[left]) left = mid + 1; <br>
    case [3,1,2]
    Your answer
          2
    Expected answer
          1
<br>
为什么漏掉了？

[3, 1, 2] -> [2]

实际我们想这样变:
[3, 1, 2] -> [1, 2] nums[left] < nums[right] return nums[left]

怎么改？
if (nums[mid] < nums[right]) right = mid;
正因为right = mid这样写，所以把当前right这个点也囊括进去，不想left = mid + 1, 直接跳过 left这个点.
