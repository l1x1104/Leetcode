[迷宫](https://leetcode.com/problems/the-maze/description/)

```java
class Solution {
    public boolean hasPath(int[][] maze, int[] start, int[] destination) {
        int m = maze.length, n = maze[0].length;
        if (maze == null || m == 0 || n == 0) {
            return true;
        }
        boolean[][] visited = new boolean[m][n];
        return dfs(maze, start, visited, destination);
    }
    private boolean dfs(int[][] maze, int[] start, boolean[][] visited, int[] destination) {
        if (start[0] == destination[0] && start[1] == destination[1]) {
            return true;
        }
        if (visited[start[0]][start[1]]) {
            return false;
        }
        
        visited[start[0]][start[1]] = true;
        
        // 0 up, 1 right, 2 down, 3 left
        for (int i = 0; i < 4; i++) {
            int[] next = helper(maze, start, i);
            if (dfs(maze, next, visited, destination)) {
                return true;
            }
        }
        
        return false;
    }
    private int[] helper(int[][] maze, int[] start, int dir) {
        int x = start[0], y = start[1];
        //int[] result = new int[2];
        switch(dir) {
            case 0:
                while (x > 0 && maze[x - 1][y] != 1) {
                    x--;
                }
                break;
            case 1: 
                while (y < maze[0].length - 1 && maze[x][y + 1] != 1) {
                    y++;
                }
                break;
            case 2:
                while (x < maze.length - 1 && maze[x + 1][y] != 1) {
                    x++;
                }
                break;
            case 3:
                while (y > 0 && maze[x][y - 1] != 1) {
                    y--;
                }
                break;
            default: 
                break;
        }
        
        return new int[]{x, y};
    }
}
```
