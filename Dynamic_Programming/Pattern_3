# Dynamic Programming Pattern 3: Longest Common Subsequence (LCS)

The **Longest Common Subsequence (LCS) Pattern** is a foundational DP pattern for problems involving two (or more) sequences, usually strings or arrays. Many real-world and interview problems are built on top of this pattern, especially those involving matching, editing, or comparing sequences.

---

## 1. **Pattern Description**

- You are given two sequences and need to find the "best" way to align, match, or edit them.
- The solution typically involves comparing elements at certain positions and making a decision (match, skip, replace, etc.).
- The classic example is the **Longest Common Subsequence** problem.

---

## 2. **Problem Examples**

- Longest Common Subsequence
- Longest Palindromic Subsequence
- Edit Distance (Levenshtein Distance)
- Shortest Common Supersequence
- Distinct Subsequences
- Longest Repeating Subsequence

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- For two indices `i` and `j` on two strings/arrays:
  - If `A[i] == B[j]`, consider including this character in the result.
  - Otherwise, move forward in either sequence (try both possibilities).
- Example (LCS):
  ```
  dp[i][j] = 1 + dp[i-1][j-1]       if A[i-1] == B[j-1]
           = max(dp[i-1][j], dp[i][j-1])   otherwise
  ```
- Usually, you use two pointers (indices) for two sequences.

### Step 2: **Decide the Method**
- **Recursive (Brute Force):** Try all possibilities by matching or skipping characters.
- **Memoization (Top-Down DP):** Store results for subproblems (`i, j` pairs).
- **Tabulation (Bottom-Up DP):** Build a 2D DP table.
- **Space Optimization:** For some problems, you can use two 1D arrays instead of a 2D array.

---

## 4. **Key Points While Coding (Java)**

- **DP Table Dimensions:** Most problems use `dp[i][j]` for positions in the two sequences.
- **Base Cases:** Usually when either string is empty (`i == 0` or `j == 0`).
- **Initialization:** Properly initialize the first row and column of the DP table.
- **Memoization Array:** Use `-1` for uncomputed values.
- **String Indices:** Be careful with 0-based vs. 1-based indexing.
- **Traceback:** For reconstructing the actual subsequence or edit operations, trace your choices backward.
- **Edge Cases:** Handle empty strings or arrays.

---

## 5. **Template Code Examples (Java)**

### a) Recursive (Brute Force) — Not for large inputs

```java
int lcs(String a, String b, int i, int j) {
    if (i == 0 || j == 0) return 0;
    if (a.charAt(i-1) == b.charAt(j-1))
        return 1 + lcs(a, b, i-1, j-1);
    else
        return Math.max(lcs(a, b, i-1, j), lcs(a, b, i, j-1));
}
```

### b) Memoization (Top-Down DP)

```java
int lcs(String a, String b, int i, int j, int[][] memo) {
    if (i == 0 || j == 0) return 0;
    if (memo[i][j] != -1) return memo[i][j];
    if (a.charAt(i-1) == b.charAt(j-1))
        memo[i][j] = 1 + lcs(a, b, i-1, j-1, memo);
    else
        memo[i][j] = Math.max(lcs(a, b, i-1, j, memo), lcs(a, b, i, j-1, memo));
    return memo[i][j];
}
// Usage:
int[][] memo = new int[a.length()+1][b.length()+1];
for (int[] row : memo) Arrays.fill(row, -1);
```

### c) Tabulation (Bottom-Up DP)

```java
int lcs(String a, String b) {
    int m = a.length(), n = b.length();
    int[][] dp = new int[m+1][n+1];
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            if (i == 0 || j == 0)
                dp[i][j] = 0;
            else if (a.charAt(i-1) == b.charAt(j-1))
                dp[i][j] = 1 + dp[i-1][j-1];
            else
                dp[i][j] = Math.max(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m][n];
}
```

### d) Space Optimized

```java
int lcs(String a, String b) {
    int m = a.length(), n = b.length();
    int[] prev = new int[n+1];
    int[] curr = new int[n+1];
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (a.charAt(i-1) == b.charAt(j-1))
                curr[j] = 1 + prev[j-1];
            else
                curr[j] = Math.max(prev[j], curr[j-1]);
        }
        int[] temp = prev; prev = curr; curr = temp;
    }
    return prev[n];
}
```

---

## 6. **Typical Interview Questions**

- How do you derive the recurrence relation for comparing sequences?
- What are your base cases and how do you initialize the DP table?
- Can you reconstruct the actual LCS string?
- How does your approach change for similar problems (e.g., edit distance, distinct subsequences)?
- Can you optimize the space complexity?

---

## 7. **Practice Problems**

1. [Longest Common Subsequence (LeetCode)](https://leetcode.com/problems/longest-common-subsequence/)
2. [Longest Palindromic Subsequence (LeetCode)](https://leetcode.com/problems/longest-palindromic-subsequence/)
3. [Edit Distance (LeetCode)](https://leetcode.com/problems/edit-distance/)
4. [Shortest Common Supersequence (LeetCode)](https://leetcode.com/problems/shortest-common-supersequence/)
5. [Distinct Subsequences (LeetCode)](https://leetcode.com/problems/distinct-subsequences/)
6. [Longest Repeating Subsequence (GFG)](https://www.geeksforgeeks.org/longest-repeating-subsequence/)

---

## 8. **Summary Table**

| Method         | Time Complexity   | Space Complexity | Pros           | Cons                 |
|----------------|------------------|------------------|----------------|----------------------|
| Recursive      | O(2^(m+n))       | O(m+n)           | Simple         | Very slow, repeats   |
| Memoization    | O(m * n)         | O(m * n)         | Fast, Easy     | Uses DP array        |
| Tabulation     | O(m * n)         | O(m * n)         | Fast           | Uses DP array        |
| Space Opt.     | O(m * n)         | O(n)             | Efficient      | Only for length      |

*(m = length of first string, n = length of second string)*

---

## 9. **Visualization**

- Draw the recursion tree for small strings.
- Show how the DP table (2D array) fills up in tabulation.
- Highlight the path taken to reconstruct the actual subsequence.

---

**Tip:**  
Always clearly define your subproblem (indices in both strings/arrays), and draw a table for a few small cases before coding!
