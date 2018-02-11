[找全排列](https://leetcode.com/problems/find-permutation/description/) <br>
通过观察，我们需要记录 D 的起始位置 i，还有 D 的连续个数 k，那么我们只需要在数组中倒置 [i, i+k] 之间的数字即可
```java
class Solution {
    public int[] findPermutation(String s) {
        int n = s.length(), cnt = 0;
        int[] nums = new int[n + 1];
        
        for (int i = 0 ; i < nums.length; i++) {
            nums[i] = i + 1;
        }
        
        char[] ch = s.toCharArray();
        for (int i = 0; i < n; i++) {
            if (ch[i] == 'D') {
                int j = i;
                while (i < n && ch[i] == 'D') {
                    i++;
                }
                reverse(nums, j, i);
                i--;
            }
        }
        
        return nums;
    }
    private void reverse(int[] ch, int start, int end) {
        for (; start < end; start++, end--) {
            int tmp = ch[end];
            ch[end] = ch[start];
            ch[start] = tmp;
        }
    }
}
```
