

# We make DP array of size n+1:

- To represent base cases (like 0 items, 0 steps, or empty string).
- To align with 1-based indexing.
- To make transition formulas cleaner (no special handling for boundaries).
- To avoid index out of range errors.

---
# 📘 Dynamic Programming: 1D vs 2D DP

## 🔹 General Rule
- **1D DP →** when the state depends on **one variable**.  
- **2D DP →** when the state depends on **two variables**.  
- Higher dimensions (3D, etc.) if more states are involved.  

---

## ✅ 1D DP
### When to Use
- State depends on **one index/state**.  
- Usually linear progression (arrays, sequences, 1D paths).  

### Examples
1. **Fibonacci Numbers**  
   - State: `i` (nth number).  
   - Recurrence:  
     ``` 
     dp[i] = dp[i-1] + dp[i-2]
     ```

2. **Climbing Stairs**  
   - State: `i` (steps).  
   - Recurrence:  
     ``` 
     dp[i] = dp[i-1] + dp[i-2]
     ```

3. **Maximum Subarray (Kadane’s Algorithm)**  
   - State: `i` (end index of subarray).  
   - Recurrence:  
     ``` 
     dp[i] = max(nums[i], nums[i] + dp[i-1])
     ```

---

## ✅ 2D DP
### When to Use
- State depends on **two indices/states**.  
- Common in **Knapsack, LCS, Edit Distance**.  

### Examples
1. **0/1 Knapsack**  
   - State: `(i, w)` → item index, weight capacity.  
   - Recurrence:  
     ``` 
     dp[i][w] = max(dp[i-1][w], dp[i-1][w - weight[i]] + value[i])
     ```

2. **Longest Common Subsequence (LCS)**  
   - State: `(i, j)` → indices of two strings.  
   - Recurrence:  
     ```
     if s1[i] == s2[j]:
         dp[i][j] = 1 + dp[i-1][j-1]
     else:
         dp[i][j] = max(dp[i-1][j], dp[i][j-1])
     ```

3. **Edit Distance**  
   - State: `(i, j)` → operations needed for prefixes of two strings.  
   - Recurrence involves **insert, delete, replace** operations.  

---

## 🔹 Space Optimization
- Many **2D DPs can be reduced to 1D** by keeping only the current & previous row.  

### Example: Knapsack (optimized)  

---
---
---

# “must-practice” problems for each major dynamic programming (DP) pattern.
---

## 1. **Fibonacci / Climbing Stairs Pattern**

1. [Climbing Stairs (LeetCode)](https://leetcode.com/problems/climbing-stairs/)
2. [Fibonacci Number (LeetCode)](https://leetcode.com/problems/fibonacci-number/)
3. [Min Cost Climbing Stairs (LeetCode)](https://leetcode.com/problems/min-cost-climbing-stairs/)
4. [Friends Pairing Problem (GFG)](https://www.geeksforgeeks.org/friends-pairing-problem/)
5. [N-th Tribonacci Number (LeetCode)](https://leetcode.com/problems/n-th-tribonacci-number/)
6. [Decode Ways (LeetCode)](https://leetcode.com/problems/decode-ways/)

---

## 2. **0/1 Knapsack Pattern**

1. [0/1 Knapsack Problem (GFG)](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)
2. [Subset Sum Problem (GFG)](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)
3. [Partition Equal Subset Sum (LeetCode)](https://leetcode.com/problems/partition-equal-subset-sum/)
4. [Target Sum (LeetCode)](https://leetcode.com/problems/target-sum/)
5. [Count of Subset Sum (GFG)](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)
6. [Last Stone Weight II (LeetCode)](https://leetcode.com/problems/last-stone-weight-ii/)

---

## 3. **Longest Common Subsequence (LCS) Pattern**

1. [Longest Common Subsequence (LeetCode)](https://leetcode.com/problems/longest-common-subsequence/)
2. [Longest Palindromic Subsequence (LeetCode)](https://leetcode.com/problems/longest-palindromic-subsequence/)
3. [Edit Distance (LeetCode)](https://leetcode.com/problems/edit-distance/)
4. [Shortest Common Supersequence (LeetCode)](https://leetcode.com/problems/shortest-common-supersequence/)
5. [Distinct Subsequences (LeetCode)](https://leetcode.com/problems/distinct-subsequences/)
6. [Longest Repeating Subsequence (GFG)](https://www.geeksforgeeks.org/longest-repeating-subsequence/)

---

## 4. **Palindrome Pattern**

1. [Longest Palindromic Substring (LeetCode)](https://leetcode.com/problems/longest-palindromic-substring/)
2. [Palindrome Partitioning II (LeetCode)](https://leetcode.com/problems/palindrome-partitioning-ii/)
3. [Count Different Palindromic Subsequences (LeetCode)](https://leetcode.com/problems/count-different-palindromic-subsequences/)
4. [Minimum Number of Cuts for Palindrome Partitioning (GFG)](https://www.geeksforgeeks.org/minimum-number-of-cuts-needed-for-a-palindrome-partition/)
5. [Palindromic Substrings (LeetCode)](https://leetcode.com/problems/palindromic-substrings/)
6. [Longest Palindromic Subsequence (LeetCode)](https://leetcode.com/problems/longest-palindromic-subsequence/)

---

## 5. **Coin Change / Minimum Coin Change Pattern**

1. [Coin Change (LeetCode)](https://leetcode.com/problems/coin-change/)
2. [Coin Change II (LeetCode)](https://leetcode.com/problems/coin-change-ii/)
3. [Minimum Coins to Make a Value (GFG)](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)
4. [Number of Ways to Make Change (GFG)](https://www.geeksforgeeks.org/coin-change-dp-7/)
5. [Combination Sum IV (LeetCode)](https://leetcode.com/problems/combination-sum-iv/)
6. [Perfect Squares (LeetCode)](https://leetcode.com/problems/perfect-squares/)

---

## 6. **Unbounded Knapsack Pattern**

1. [Unbounded Knapsack (GFG)](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-items-allowed/)
2. [Rod Cutting (LeetCode)](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/)
3. [Coin Change II (LeetCode)](https://leetcode.com/problems/coin-change-ii/)
4. [Integer Break (LeetCode)](https://leetcode.com/problems/integer-break/)
5. [Word Break (LeetCode)](https://leetcode.com/problems/word-break/)
6. [Minimum Coins to Make a Value (GFG)](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)

---

## 7. **Matrix DP / Grid DP Pattern**

1. [Unique Paths (LeetCode)](https://leetcode.com/problems/unique-paths/)
2. [Minimum Path Sum (LeetCode)](https://leetcode.com/problems/minimum-path-sum/)
3. [Longest Increasing Path in a Matrix (LeetCode)](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/)
4. [Maximum Square (LeetCode)](https://leetcode.com/problems/maximal-square/)
5. [Cherry Pickup (LeetCode)](https://leetcode.com/problems/cherry-pickup/)
6. [Dungeon Game (LeetCode)](https://leetcode.com/problems/dungeon-game/)

---

## 8. **Subarray / Subsequence Pattern**

1. [Maximum Subarray (LeetCode)](https://leetcode.com/problems/maximum-subarray/)
2. [Longest Increasing Subsequence (LeetCode)](https://leetcode.com/problems/longest-increasing-subsequence/)
3. [Maximum Product Subarray (LeetCode)](https://leetcode.com/problems/maximum-product-subarray/)
4. [Number of Longest Increasing Subsequence (LeetCode)](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)
5. [Longest Continuous Increasing Subsequence (LeetCode)](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)
6. [Longest Bitonic Subsequence (GFG)](https://www.geeksforgeeks.org/longest-bitonic-subsequence-dp-15/)

---

## 9. **Bitmask DP**

1. [Count Number of Ways to Place N Queens (LeetCode)](https://leetcode.com/problems/n-queens-ii/)
2. [Partition to K Equal Sum Subsets (LeetCode)](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)
3. [Minimum Number of Work Sessions to Finish the Tasks (LeetCode)](https://leetcode.com/problems/minimum-number-of-work-sessions-to-finish-the-tasks/)
4. [Travelling Salesman Problem (GFG)](https://www.geeksforgeeks.org/travelling-salesman-problem-set-1/)
5. [Smallest Sufficient Team (LeetCode)](https://leetcode.com/problems/smallest-sufficient-team/)
6. [Minimum Incompatibility (LeetCode)](https://leetcode.com/problems/minimum-incompatibility/)

---

## 10. **Interval DP**

1. [Burst Balloons (LeetCode)](https://leetcode.com/problems/burst-balloons/)
2. [Matrix Chain Multiplication (GFG)](https://www.geeksforgeeks.org/matrix-chain-multiplication-dp-8/)
3. [Palindrome Partitioning II (LeetCode)](https://leetcode.com/problems/palindrome-partitioning-ii/)
4. [Minimum Cost to Merge Stones (LeetCode)](https://leetcode.com/problems/minimum-cost-to-merge-stones/)
5. [Scramble String (LeetCode)](https://leetcode.com/problems/scramble-string/)
6. [Optimal BST (GFG)](https://www.geeksforgeeks.org/optimal-binary-search-tree-dp-24/)

---

Would you like these as a downloadable Markdown file or in any other format for easy reference?
