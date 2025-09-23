# Problem: Surrounded Regions

## 📄 Problem Statement
Write the exact statement in your own words.  
(Add constraints if any, e.g., "1 <= nums.length <= 10^4")

---

## 🧠 Brute Force Approach
### Idea
- if someone is on the boundary, that is where it is not covered
- if they are not by the boundary, it is bound to surrounded by x
- start from boundary zeros and mark them that they will not be converted
- convert the remaining 0
- dfs

### Code
```java
// Brute force solution
public void solve(char[][] board) {
    int n = board.length;
    int m = board[0].length;
    int vis[][] = new int[n][m];
    int delrow[] = {-1, 0, 1, 0};
    int delcol[] = {0, 1, 0, -1};
    for (int j = 0; j<m; j++) {
        // first row
        if (board[0][j] == 'O' && vis[0][j] == 0)
            dfs(board, 0, j, delrow, delcol, vis, n, m);
        // last row
        if (board[n-1][j] == 'O' && vis[n-1][j] == 0)
            dfs(board, n-1, j, delrow, delcol, vis, n, m);
    }

    for (int i = 0; i<n; i++) {
        // first col
        if (board[i][0] == 'O' && vis[i][0] == 0)
            dfs(board, i, 0, delrow, delcol, vis, n, m);
        // last col
        if (board[i][m-1] == 'O' && vis[i][m-1] == 0)
            dfs(board, i, m-1, delrow, delcol, vis, n, m);
    }

    for (int i = 0; i<n; i++) {
        for (int j= 0; j<m; j++) {
            if (vis[i][j] == 0 && board[i][j] == 'O')
                board[i][j] = 'X';
        }
    }
}

public void dfs (char[][] board, int row, int col, int[] delrow, int[] delcol, int[][] vis, int n, int m) {
    vis[row][col] = 1;
    for (int i = 0; i<4; i++) {
        int nrow = row+delrow[i];
        int ncol = col+delcol[i];
        if (nrow>=0 && ncol>=0 && nrow<n && ncol<m && board[nrow][ncol] == 'O' && vis[nrow][ncol] == 0)
            dfs(board, nrow, ncol, delrow, delcol, vis, n, m);
    }
}
```

### Complexity
- **Time:** O(nxmx4) dfs + o(n) boundaries -> o(nxm)
- **Space:** O(nxm)
