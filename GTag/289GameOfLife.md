[生命游戏](https://leetcode.com/problems/game-of-life/description/)

in-place <br>
状态 0： 死细胞转为死细胞 <br>   00
状态 1： 活细胞转为活细胞 <br>   11
状态 2： 活细胞转为死细胞 <br>   10 
状态 3： 死细胞转为活细胞 <br>   01

```java
class Solution {
    public void gameOfLife(int[][] board) {
        int m = board.length, n = board[0].length;
        int[] dx = {-1, -1, -1, 0, 1, 1, 1, 0};
        int[] dy = {-1, 0, 1, 1, 1, 0, -1, -1};
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int cnt = 0;
                for (int k = 0; k < 8; k++) {
                    int x = i + dx[k], y = j + dy[k];
                    if (x >= 0 && y >= 0 && x < m && y < n && (board[x][y] == 1 || board[x][y] == 2)) {
                        cnt++;
                    }
                }
                if (board[i][j] == 1 && (cnt < 2 || cnt > 3)) {
                    board[i][j] = 2;
                } else if (board[i][j] == 0 && cnt == 3) {
                    board[i][j] = 3;
                }
            }
        }
        
        for (int i = 0; i < m; ++i) {
            for (int j = 0; j < n; ++j) {
                board[i][j] %= 2;
            }
        }
    }
}
```
