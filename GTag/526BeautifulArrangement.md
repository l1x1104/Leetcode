[优美排列](https://leetcode.com/problems/beautiful-arrangement/description/)

- Solution 1: Backtracking
```java
class Solution {
    public int countArrangement(int N) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> tmpList = new ArrayList<>();
        boolean[] used  = new boolean[N + 1];
        if(N == 0 || N == 1) {
            return N;
        }
        helper(N, 1, res, tmpList);
        return res.size();
    }
    public void helper(int N, int pos, List<List<Integer>> res, List<Integer> tmpList) {
        if(N == tmpList.size()) {
            res.add(new ArrayList<>(tmpList));
            return;
        }
        for(int i = 1; i <= N; i++) {
            if(tmpList.contains(i)) {
                continue;
            }else if(i % pos == 0 || pos % i == 0) {
                tmpList.add(i);
                helper(N, pos + 1, res, tmpList);
                tmpList.remove(tmpList.size() - 1);
            }
        }
    }
}
```

- Solution 2: 交换数组中任意两个数字的位置
```java
class Solution {
    public int countArrangement(int N) {
        int[] nums = new int[N];
        for (int i = 0; i < N; i++) {
            nums[i] = i + 1;
        }
        
        return helper(N, nums);
    }
    private int helper(int n, int[] nums) {
        if (n <= 0) {
            return 1;
        }
        int res = 0;
        for (int i = 0; i < n; i++) {
            if (n % nums[i] == 0 || nums[i] % n == 0) {
                swap(nums, i, n - 1);
                res += helper(n - 1, nums);
                swap(nums, i, n - 1);
            }
        }
        
        return res;
    }
    private void swap(int[] nums, int i, int j) {
        int tmp = nums[j];
        nums[j] = nums[i];
        nums[i] = tmp;
    }
}
```
