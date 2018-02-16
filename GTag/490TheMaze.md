[迷宫](https://leetcode.com/problems/the-maze/description/)
```
There is a ball in a maze with empty spaces and walls. The ball can go through empty spaces by rolling up, down, left or right, but it won't stop rolling until hitting a wall. When the ball stops, it could choose the next direction.

Given the ball's start position, the destination and the maze, determine whether the ball could stop at the destination.

The maze is represented by a binary 2D array. 1 means the wall and 0 means the empty space. You may assume that the borders of the maze are all walls. The start and destination coordinates are represented by row and column indexes.

Example 1

Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (4, 4)

Output: true
Explanation: One possible way is : left -> down -> left -> down -> right -> down -> right.

Example 2

Input 1: a maze represented by a 2D array

0 0 1 0 0
0 0 0 0 0
0 0 0 1 0
1 1 0 1 1
0 0 0 0 0

Input 2: start coordinate (rowStart, colStart) = (0, 4)
Input 3: destination coordinate (rowDest, colDest) = (3, 2)

Output: false
Explanation: There is no way for the ball to stop at the destination.

Note:
There is only one ball and one destination in the maze.
Both the ball and the destination exist on an empty space, and they will not be at the same position initially.
The given maze does not contain border (like the red rectangle in the example pictures), but you could assume the border of the maze are all walls.
The maze contains at least 2 empty spaces, and both the width and height of the maze won't exceed 100.
```

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
