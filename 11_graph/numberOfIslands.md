# Problem: Number of Islands

## 📄 Problem Statement
Given an m x n 2D binary grid which represents a map of 
'1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. 
You may assume all four edges of the grid are all surrounded by water.

---

## 🧠 Brute Force Approach
### Idea
- can implement any of the traversals - bfs or dfs
- in dfs, the number of calls to the recursive function would mean - number of islands (but the starting node would be multiple different)
- need to figure out starting nodes
- keep track of visited array

### Code
```java
// Brute force solution
// dfs
public int numIslands(char[][] grid) {
    int n = grid.length;
    int m = grid[0].length;
    boolean vis[][] = new boolean[n][m];
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (!vis[i][j] && grid[i][j] == '1') {
                count++;
                dfs(grid, vis, i, j);
            }
        }
    }
    return count;
}

public void dfs(char[][] grid, boolean[][] vis, int row, int col) {
    int n = grid.length;
    int m = grid[0].length;
    if (row < 0 || row >= n || col < 0 || col >= m || vis[row][col] || grid[row][col] == '0') {
        return;
    }
    vis[row][col] = true;
    dfs(grid, vis, row + 1, col);
    dfs(grid, vis, row - 1, col);
    dfs(grid, vis, row, col + 1);
    dfs(grid, vis, row, col - 1);
}
```

### Complexity
- **Time:** O(n^2) ?
- **Space:** O(n^2) ?

---


```java
// bfs
```