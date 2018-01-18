***
#### Generate a random MxN starting board. It cannot have 3 or more pieces in a row (horizontally or vertically) of the same color. K colors.

##### Algorithm:
- 这个题看起来根本不需要back tracking， 枚举每一个位置的时候你有k个color可以选择，如果上面两个是一样的，那么k个color要删除这个颜色，如果左面两个color是一样的，你要删除这个颜色，剩下的颜色你都可以用.

```java
    public int[][] kColorBoard(int m, int n, int k) {
        int[][] res = new int[m][n];
        List<Integer> colors = new ArrayList<>();
        Random random = new Random();
        for (int i = 0; i < k; i++) {
            colors.add(i);
        }
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                List<Integer> avl_colors = new ArrayList<>(colors);
                for (int l = 0; l < k; l++) {
                    int color = avl_colors.get(random.nextInt(avl_colors.size()));
                    boolean col_check = false, row_check = false;
                    if (i > 1) {
                        col_check = res[i - 1][j] == color && res[i - 2][j] == color;
                    }
                    if (j > 1) {
                        row_check = res[i][j - 1] == color && res[i][j - 2] == color;
                    }
                    if (col_check || row_check) {
                        avl_colors.remove(color);
                        continue;
                    }
                    res[i][j] = color;
                    break;
                }
            }
        }
        return res;
    }
```
