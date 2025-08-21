# Dynamic Programming Pattern 7: Matrix/Grid DP Pattern

The **Matrix/Grid DP Pattern** is crucial for problems involving grids or matrices, where you need to compute the optimal path, area, or count within a 2D space. This pattern leverages relationships between neighboring cells, making it ideal for pathfinding, area maximization, or dynamic counting in two dimensions.

---

## 1. **Pattern Description**

- You are given a 2D grid/matrix (of costs, values, obstacles, etc.).
- The objective is often to find the minimum/maximum path sum, count paths, or find the largest submatrix with some property.
- Moves are usually restricted to right, down, or both, but some problems allow movement in more directions.

---

## 2. **Problem Examples**

- Unique Paths
- Minimum Path Sum
- Unique Paths with Obstacles
- Longest Increasing Path in a Matrix
- Maximal Square
- Cherry Pickup
- Dungeon Game

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- Relate each cell to its neighbors (usually top, left, or both).
- Example (Minimum Path Sum):  
  `dp[i][j] = grid[i][j] + min(dp[i-1][j], dp[i][j-1])`
- Example (Unique Paths):  
  `dp[i][j] = dp[i-1][j] + dp[i][j-1]`

### Step 2: **Choose the Method**
- **Tabulation (Bottom-Up DP):** Most common; fill a 2D DP array from top-left to bottom-right.
- **Space Optimization:** Use a 1D array if only the previous row/column is needed.
- **Memoization/Recursion:** Good for small grids or when learning.

---

## 4. **Key Points While Coding (Java)**

- **DP Table Size:** Use `dp[m][n]` for `m` rows and `n` columns.
- **Base Cases:** Set first row and first column appropriately (often to 1 for path counts).
- **Obstacles/Constraints:** For problems with obstacles, set `dp[i][j]=0` where blocked.
- **Order of Filling:** Usually row by row or column by column.
- **Boundary Checks:** Always check that indices are within bounds for neighbors.
- **Variable Movement:** If allowed, adjust the recurrence (e.g., for diagonal moves).
- **Space Optimization:** Use 1D arrays when only the previous row/column matters.
- **Traceback:** For path reconstruction, keep a parent pointer or traceback info.

---

## 5. **Template Code Examples (Java)**

### a) Unique Paths

```java
int uniquePaths(int m, int n) {
    int[][] dp = new int[m][n];
    for (int i = 0; i < m; i++) dp[i][0] = 1;
    for (int j = 0; j < n; j++) dp[0][j] = 1;
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = dp[i-1][j] + dp[i][j-1];
        }
    }
    return dp[m-1][n-1];
}
```

### b) Minimum Path Sum

```java
int minPathSum(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    int[][] dp = new int[m][n];
    dp[0][0] = grid[0][0];
    for (int i = 1; i < m; i++) dp[i][0] = dp[i-1][0] + grid[i][0];
    for (int j = 1; j < n; j++) dp[0][j] = dp[0][j-1] + grid[0][j];
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[i][j] = grid[i][j] + Math.min(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m-1][n-1];
}
```

### c) Maximal Square

```java
int maximalSquare(char[][] matrix) {
    int m = matrix.length, n = matrix[0].length, max = 0;
    int[][] dp = new int[m+1][n+1];
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (matrix[i-1][j-1] == '1') {
                dp[i][j] = 1 + Math.min(Math.min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]);
                max = Math.max(max, dp[i][j]);
            }
        }
    }
    return max * max;
}
```

### d) Space Optimized (for Unique Paths)

```java
int uniquePaths(int m, int n) {
    int[] dp = new int[n];
    Arrays.fill(dp, 1);
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[j] += dp[j-1];
        }
    }
    return dp[n-1];
}
```

---

## 6. **Key Things to Remember**

- Always initialize the first row and column based on the problem statement (often all 1s for path problems).
- Set `dp[i][j]=0` for obstacles or blocked paths.
- For path sum problems, base cases may be set to a large number (for min) or zero (for max).
- If movement is allowed in more than two directions, adjust recurrence accordingly.
- For counting paths, be careful with overflow if the grid is large.
- Use space optimization when only previous row/column matters.
- For reconstruction, maintain a parent/traceback array if required.

---

## 7. **Practice Problems**

1. [Unique Paths (LeetCode)](https://leetcode.com/problems/unique-paths/)
2. [Minimum Path Sum (LeetCode)](https://leetcode.com/problems/minimum-path-sum/)
3. [Unique Paths II (LeetCode)](https://leetcode.com/problems/unique-paths-ii/)
4. [Longest Increasing Path in a Matrix (LeetCode)](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)
5. [Maximal Square (LeetCode)](https://leetcode.com/problems/maximal-square/)
6. [Dungeon Game (LeetCode)](https://leetcode.com/problems/dungeon-game/)
7. [Cherry Pickup (LeetCode)](https://leetcode.com/problems/cherry-pickup/)

---

## 8. **Summary Table**

| Problem Type       | Time Complexity | Space Complexity | DP State      |
|--------------------|----------------|------------------|---------------|
| Unique Paths       | O(m*n)         | O(m*n) or O(n)   | dp[i][j]      |
| Min Path Sum       | O(m*n)         | O(m*n) or O(n)   | dp[i][j]      |
| Maximal Square     | O(m*n)         | O(m*n)           | dp[i][j]      |

*(m = number of rows, n = number of columns)*

---

## 9. **Visualization**

- Draw the DP table for a small grid, showing how each cell is filled.
- Highlight allowed movements (e.g., right and down) in the recurrence.
- Trace a sample path for minimum/maximum path problems.

---

**Tip:**  
Carefully set up your base cases and always check for out-of-bounds errors. For problems involving obstacles, handle zeros or blockages early in your DP logic!
