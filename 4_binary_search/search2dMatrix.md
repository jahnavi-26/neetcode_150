# Problem: Search a 2D matrix

## 📄 Problem Statement
given nxm matrix with following properties:
- Each row is sorted in non-decreasing order. 
- The first integer of each row is greater than the last integer of the previous row.

return true if target is present in the matrix else return false
O(log(m * n)) - time complexity
---

## 🧠 Brute Force Approach
### Idea
- iterate the matrix and compare the ele with target ele
- if found, return ture
- else return false

### Code
```java
// Brute force solution
public boolean searchMatrix(int[][] matrix, int target) {
    int n = matrix.length-1;
    int m = matrix[0].length-1;
    for (int i = 0; i<n; i++) {
        for (int j = 0; j<m; j++) {
            if (matrix[i][j] == target) return true;
        }
    }
    return false;
}
```

### Complexity
- **Time:** O(n*m)
- **Space:** O(1)

---

## 🧪 Optimal Approach
### Idea
- the matrix is sorted in ascending order
- start from [0][m] - top right (or [n][0] - bottom left)
- if the ele is equal to target, return true
- if the ele is lesser that target, decrease the column
- if it is more than target, increase row

### Code
```java
// optimal force solution
public boolean searchMatrix(int[][] matrix, int target) {
    int n = matrix.length;
    int m = matrix[0].length;
    int row = 0; // top right starting point
    int col = m-1;
    while (row<n && col>=0) {
        if (matrix[row][col] == target) return true;
        else if (matrix[row][col] < target) row++;
        else col--;
    }
    return false;
}
```

### Complexity
- **Time:** O(logn + logm)
- **Space:** O(1)

---
