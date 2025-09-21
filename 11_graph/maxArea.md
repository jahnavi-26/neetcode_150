# Problem: Max area of Island

## 📄 Problem Statement
You are given an m x n binary matrix grid. An island is a group of 1's (representing land)
connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value 1 on the island.

Return the maximum area of an island in grid. If there is no island, return 0.

---

## 🧠 Brute Force Approach
### Idea
- Explain your naive approach in 2–3 lines.

### Code
```java
// Brute force solution
public int maxAreaOfIsland(int[][] grid) {
    int n = grid.length;
    int m = grid[0].length;
    int maxArea = 0;
    int count = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (grid[i][j] == 1) {
                int area = dfs(grid, i, j);
                maxArea = Math.max(maxArea, area);
            }
        }
    }
    return maxArea;
}

public int dfs(int[][] grid, int row, int col) {
    int n = grid.length;
    int m = grid[0].length;

    if (row < 0 || row >= n || col < 0 || col >= m || grid[row][col] == 0) {
        return 0;
    }
    int area = 1;
    grid[row][col] = 0; // use same matrix to visit
    area += dfs(grid, row + 1, col);
    area += dfs(grid, row - 1, col);
    area += dfs(grid, row, col + 1);
    area += dfs(grid, row, col - 1);
    return area;
}
```

### Complexity
- **Time:** O(n)
  Each cell is visited at most once → O(m * n)
- **Space:** O(1)
  DFS recursion stack in worst case: O(m * n) (if grid is full of 1s).

---