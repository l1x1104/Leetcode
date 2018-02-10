[有序矩阵中第K小的元素](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

- Solution 1: BS
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int low = matrix[0][0], high = matrix[n - 1][n - 1];
        while (low < high) {
            int mid = (low + high) / 2;
            int count = count(matrix, mid);
            if (count < k) {
                low = mid + 1;
            }else {
                high = mid;
            }
        }                                            
        return low;
    }
    public int count(int[][] matrix, int target) {
        int n = matrix.length, r = n - 1, c = 0;
        int sum = 0;
        while (r >= 0 && c <= n - 1) {
            if (matrix[r][c] > target) r --;
            else {
                c ++;
                sum += r + 1;
            }
        }
        return sum;
    }                                                 
 }
 ```
 这算法有个问题：极端情况：k == 1,
              假如第一个和最后数相差非常大，每次mid值都很大，逼近第一个数非常慢，worse case复杂度O(n^2). 不如暴力解O(n).
 
- Solution 2: Priority Queue
```java
 class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>(k, new Comparator<Integer>(){
            @Override
            public int compare(Integer a, Integer b) {
                return b - a;
            }
        });
        int count = 0;
        for (int i = 0; i <= n - 1; i++) {
            for (int j = 0; j <= n - 1; j++) {
                if (count < k) {
                    count ++;
                    pq.offer(matrix[i][j]);
                }else {
                    if (pq.peek() > matrix[i][j]) {
                        pq.poll();
                        pq.offer(matrix[i][j]);
                    }
                }
            }
        }
        return pq.peek();
    }                                                
 }
 
```
