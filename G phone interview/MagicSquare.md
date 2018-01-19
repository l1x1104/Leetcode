***
#### 在一个m*n的矩阵里面找出数magic square的个数。magic square指的是行，列，对角反对角之和相等。非常straight forward的一题

* In any magic square, the first number i.e. 1 is stored at position (n/2, n-1). Let this position be (i,j). 
- The next number is stored at position (i-1, j+1) where we can consider each row & column as circular array i.e. they wrap around.
- Three conditions hold:
1. 下一个数的坐标(row - 1, column + 1). 如果row == -1, 置为最底下一层. column == n.length，归为0.
2. 如果走到的地方已经有数存在，column -= 2 && row += 1.
3. 如果走到最右上角, (row == -1 && column == n)，坐标为(0, n - 2);
<br>
```java
public void generateSquare(int n) {
    int[][] magicSquare = new int[n][n];
    
    int i = n/2, j = n-1; // initial 1
    for (int num = 1; num <= n * n; num++) {
        if (i == -1 && j == n) {
            i = 0;
            j = n - 2;
        } else {
            if (j == n) {
                j = 0;
            }
            if (i == -1) {
                i = n;
            }
        }
        if (magicSquare[i][j] != 0) {
            j -= 2;
            i ++;
            continue;
        } 
        magicSquare[i][j] = num; 
        i --;
        j ++;
    }
}    
```
