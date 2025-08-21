# Dynamic Programming Pattern 4: Palindrome Pattern

The **Palindrome Pattern** in dynamic programming covers problems involving palindromic substrings, subsequences, and partitioning. These problems often require checking if a substring is a palindrome or finding the optimal way to partition or modify a string to achieve palindromic properties.

---

## 1. **Pattern Description**

- You are given a string and need to find or count palindromic substrings or subsequences, or partition/transform the string with palindromic constraints.
- Classic examples include **Longest Palindromic Substring**, **Palindrome Partitioning II**, and **Longest Palindromic Subsequence**.

---

## 2. **Problem Examples**

- Longest Palindromic Substring
- Palindrome Partitioning II (minimum cuts)
- Count Different Palindromic Subsequences
- Minimum Number of Cuts for Palindrome Partitioning
- Palindromic Substrings (count all)
- Longest Palindromic Subsequence

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- For substring problems, often use two pointers: `start` and `end`.
- For subsequence problems, use indices to represent the current subproblem.
- Example (Longest Palindromic Substring / Subsequence):
  ```
  dp[i][j] = true if s.charAt(i) == s.charAt(j) && (j-i < 2 || dp[i+1][j-1])
  ```
  or
  ```
  dp[i][j] = 2 + dp[i+1][j-1] if s.charAt(i) == s.charAt(j)
           = max(dp[i+1][j], dp[i][j-1]) otherwise
  ```

### Step 2: **Decide the Method**
- **Recursive (Brute Force):** Try all substrings/subsequences and check for palindrome property.
- **Memoization (Top-Down DP):** Store results for overlapping subproblems (often a 2D array).
- **Tabulation (Bottom-Up DP):** Fill a DP table, often by increasing substring length.
- **Special Handling:** For partitioning/cutting, DP may store the minimum cut count for a substring.

---

## 4. **Key Points While Coding (Java)**

- **DP Table Dimensions:** Typically use `dp[i][j]` for substring from `i` to `j`.
- **Base Cases:** Single characters are always palindromes; two-character substrings need special attention.
- **Order of Filling Table:** Fill by increasing substring length (`len` from 1 to n).
- **String Indices:** Careful with 0-based vs. 1-based indices.
- **Palindrome Checking:** Use precomputed results for subproblems to avoid recomputation.
- **Initialization:** For counting/counting distinct palindromes, initialize accordingly.

---

## 5. **Template Code Examples (Java)**

### a) Longest Palindromic Substring (Tabulation)

```java
String longestPalindrome(String s) {
    int n = s.length(), start = 0, maxLen = 1;
    boolean[][] dp = new boolean[n][n];
    for (int i = 0; i < n; i++) dp[i][i] = true; // Single char
    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;
            if (s.charAt(i) == s.charAt(j)) {
                if (len == 2 || dp[i+1][j-1]) {
                    dp[i][j] = true;
                    if (len > maxLen) {
                        start = i; maxLen = len;
                    }
                }
            }
        }
    }
    return s.substring(start, start + maxLen);
}
```

### b) Longest Palindromic Subsequence (Tabulation)

```java
int longestPalindromeSubseq(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];
    for (int i = n - 1; i >= 0; i--) {
        dp[i][i] = 1;
        for (int j = i + 1; j < n; j++) {
            if (s.charAt(i) == s.charAt(j))
                dp[i][j] = 2 + dp[i+1][j-1];
            else
                dp[i][j] = Math.max(dp[i+1][j], dp[i][j-1]);
        }
    }
    return dp[0][n-1];
}
```

### c) Palindrome Partitioning II (Minimum Cuts)

```java
int minCut(String s) {
    int n = s.length();
    boolean[][] isPal = new boolean[n][n];
    int[] cuts = new int[n];
    for (int i = 0; i < n; i++) {
        int min = i;
        for (int j = 0; j <= i; j++) {
            if (s.charAt(i) == s.charAt(j) && (i - j < 2 || isPal[j+1][i-1])) {
                isPal[j][i] = true;
                min = (j == 0) ? 0 : Math.min(min, cuts[j-1] + 1);
            }
        }
        cuts[i] = min;
    }
    return cuts[n-1];
}
```

### d) Count Palindromic Substrings

```java
int countSubstrings(String s) {
    int n = s.length(), count = 0;
    boolean[][] dp = new boolean[n][n];
    for (int i = n - 1; i >= 0; i--) {
        for (int j = i; j < n; j++) {
            if (s.charAt(i) == s.charAt(j) && (j - i < 2 || dp[i+1][j-1])) {
                dp[i][j] = true;
                count++;
            }
        }
    }
    return count;
}
```

---

## 6. **Typical Interview Questions**

- What is your DP state and how do you define dp[i][j]?
- How do you handle base cases for substrings of length 1 or 2?
- Can you optimize your algorithm’s time/space complexity?
- How would you count, rather than just find, all palindromic substrings/subsequences?
- How do you reconstruct the palindrome or partition path?

---

## 7. **Practice Problems**

1. [Longest Palindromic Substring (LeetCode)](https://leetcode.com/problems/longest-palindromic-substring/)
2. [Palindrome Partitioning II (LeetCode)](https://leetcode.com/problems/palindrome-partitioning-ii/)
3. [Count Different Palindromic Subsequences (LeetCode)](https://leetcode.com/problems/count-different-palindromic-subsequences/)
4. [Minimum Number of Cuts for Palindrome Partitioning (GFG)](https://www.geeksforgeeks.org/minimum-number-of-cuts-needed-for-a-palindrome-partition/)
5. [Palindromic Substrings (LeetCode)](https://leetcode.com/problems/palindromic-substrings/)
6. [Longest Palindromic Subsequence (LeetCode)](https://leetcode.com/problems/longest-palindromic-subsequence/)

---

## 8. **Summary Table**

| Problem Type             | Time Complexity | Space Complexity | DP State           |
|--------------------------|-----------------|------------------|--------------------|
| Palindromic Substring    | O(n^2)          | O(n^2)           | dp[i][j]: substring|
| Palindromic Subsequence  | O(n^2)          | O(n^2)           | dp[i][j]: indices  |
| Partitioning (min cuts)  | O(n^2)          | O(n^2)           | dp[i]: cuts        |
| Counting Palindromes     | O(n^2)          | O(n^2)           | dp[i][j]: count    |

---

## 9. **Visualization**

- Draw the DP table with substring start and end indices.
- Illustrate filling the table diagonally (by increasing substring length).
- Trace the recursive calls for small strings.

---

**Tip:**  
Always clearly define the meaning of your dp[i][j] state (substring or subsequence) and fill the DP table in the correct order for dependencies!
