[最大连续1的个数之二](https://leetcode.com/problems/max-consecutive-ones-ii/description/)

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int pre = 0, cnt = 0, res = 0;
        
        for (int num: nums) {
            cnt++;
            if (num == 0) {
                pre = cnt;
                cnt = 0;
            }
            res = Math.max(res, cnt + pre);
        }
        
        return res;
    }
}
```

- FollowUp: <br>
能翻转k次
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int res = 0, zero = 0, j = 0, k = 1;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) ++zero;
            while (zero > k) {
                if (nums[j++] == 0) --zero;
            }
            res = Math.max(res, i - j + 1);
        }
        return res;
    }
}
```
nums[j]需要访问之前的数字。我们可以将遇到的0的位置全都保存下来，这样我们需要移动j的时候就知道移到哪里了
```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int res = 0, j = 0, k = 1;
        Queue<Integer> q = new LinkedList<>();
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                q.offer(i);
            }
            if (q.size() > k) {
                j = q.poll() + 1;
            }
            res = Math.max(res, i - j + 1);
        }
        
        return res;
    }
}
```
