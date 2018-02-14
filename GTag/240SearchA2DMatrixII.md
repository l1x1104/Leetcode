[搜索二维矩阵之二](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)

```java
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0) {
            return false;
        }
        if(matrix[0] == null || matrix[0].length == 0) {
            return false;
        }
        int row = matrix.length, column = matrix[0].length;
        int left = 0, right = column - 1;
        while(left < row && right >= 0) {
            if(matrix[left][right] == target) {
                return true;
            }else if(matrix[left][right] > target) {
                right --;
            }else if(matrix[left][right] < target) {
                left ++;
            }
        }
        
        return false;
    }
}
```
