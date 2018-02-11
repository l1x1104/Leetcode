[找全排列](https://leetcode.com/problems/find-permutation/description/)

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
