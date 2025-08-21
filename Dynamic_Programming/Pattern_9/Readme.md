# Dynamic Programming Pattern 9: Subsequence DP Pattern

The **Subsequence DP Pattern** is used for problems where you must find or count the best (maximum, minimum, longest, etc.) non-contiguous subsequence within an array or string. Unlike subarrays/substrings, subsequences do not have to be contiguous but must maintain the original order.

---

## 1. **Pattern Description**

- You are given an array or string and must find/count the best subsequence (not necessarily contiguous).
- Common goals: maximize/minimize sum, length, or find the count of such subsequences.
- Classic examples: **Longest Increasing Subsequence (LIS)**, **Longest Decreasing Subsequence**, **Maximum Sum Increasing Subsequence**, **Number of Distinct Subsequences**, **Subset Sum**.

---

## 2. **Problem Examples**

- Longest Increasing Subsequence (LIS)
- Longest Decreasing Subsequence
- Maximum Sum Increasing Subsequence
- Number of Distinct Subsequences
- Subset Sum
- Partition Equal Subset Sum
- Longest Arithmetic Subsequence

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- For each index, decide whether to include the current element in the subsequence or not.
- **LIS Example:**
  ```
  dp[i] = max(1, dp[j] + 1) for all j < i and nums[i] > nums[j]
  ```
- **Subset Sum Example:**
  ```
  dp[i][sum] = dp[i-1][sum] || dp[i-1][sum - nums[i]]
  ```

### Step 2: **Choose the Method**
- **Tabulation (Bottom-Up DP):** Common for LIS and subset problems.
- **Memoization (Top-Down DP):** Useful for counting distinct subsequences.
- **Patience Sorting (LIS):** For LIS, patience sorting with binary search optimizes to O(n log n).

---

## 4. **Key Points While Coding (Java)**

- **DP Table Size:** For LIS and similar, use 1D array; for subset/partition use 2D array.
- **Initialization:**
  - For LIS, initialize all `dp[i] = 1` (every element is an LIS of length 1).
  - For subset sum, initialize `dp[0][0] = true`.
- **Transitions:** For each element, try including or excluding it.
- **Order:** For some problems (e.g. counting subsequences), reverse traversal avoids double-counting.
- **Space Optimization:** Many problems can be optimized to 1D DP.
- **Traceback:** To reconstruct the subsequence, keep a parent array.

---

## 5. **Template Code Examples (Java)**

### a) Longest Increasing Subsequence (O(n^2) DP)

```java
int lengthOfLIS(int[] nums) {
    int n = nums.length, maxLen = 1;
    int[] dp = new int[n];
    Arrays.fill(dp, 1);
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[i] > nums[j])
                dp[i] = Math.max(dp[i], dp[j] + 1);
        }
        maxLen = Math.max(maxLen, dp[i]);
    }
    return maxLen;
}
```

### b) Longest Increasing Subsequence (O(n log n) Patience Sorting)

```java
int lengthOfLIS(int[] nums) {
    List<Integer> tails = new ArrayList<>();
    for (int num : nums) {
        int idx = Collections.binarySearch(tails, num);
        if (idx < 0) idx = -(idx + 1);
        if (idx == tails.size()) tails.add(num);
        else tails.set(idx, num);
    }
    return tails.size();
}
```

### c) Subset Sum (Can sum be formed?)

```java
boolean canPartition(int[] nums) {
    int sum = Arrays.stream(nums).sum();
    if (sum % 2 != 0) return false;
    int target = sum / 2;
    boolean[] dp = new boolean[target + 1];
    dp[0] = true;
    for (int num : nums) {
        for (int i = target; i >= num; i--) {
            dp[i] = dp[i] || dp[i - num];
        }
    }
    return dp[target];
}
```

### d) Number of Distinct Subsequences

```java
int numDistinct(String s, String t) {
    int m = s.length(), n = t.length();
    int[][] dp = new int[m+1][n+1];
    for (int i = 0; i <= m; i++) dp[i][0] = 1;
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s.charAt(i-1) == t.charAt(j-1))
                dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
            else
                dp[i][j] = dp[i-1][j];
        }
    }
    return dp[m][n];
}
```

---

## 6. **Key Things to Remember**

- Subsequence problems allow skipping elements, but order must be preserved.
- For LIS, initialize all `dp[i] = 1` and update by looking at all previous elements.
- For subset/partition problems, reverse loop when updating 1D dp to avoid overcounting.
- Use binary search for LIS O(n log n) solution.
- For counting, carefully consider overlapping subproblems to avoid double-counting.

---

## 7. **Practice Problems**

1. [Longest Increasing Subsequence (LeetCode)](https://leetcode.com/problems/longest-increasing-subsequence/)
2. [Partition Equal Subset Sum (LeetCode)](https://leetcode.com/problems/partition-equal-subset-sum/)
3. [Number of Distinct Subsequences (LeetCode)](https://leetcode.com/problems/distinct-subsequences/)
4. [Maximum Sum Increasing Subsequence (GFG)](https://www.geeksforgeeks.org/maximum-sum-increasing-subsequence-dp-14/)
5. [Longest Arithmetic Subsequence (LeetCode)](https://leetcode.com/problems/longest-arithmetic-subsequence/)

---

## 8. **Summary Table**

| Problem Type                 | Time Complexity      | Space Complexity | DP State            |
|------------------------------|---------------------|------------------|---------------------|
| Longest Increasing Subseq    | O(n^2) / O(n log n) | O(n)             | dp[i]               |
| Subset Sum                   | O(n*target)         | O(target)        | dp[target]          |
| Num Distinct Subsequences    | O(m*n)              | O(m*n)           | dp[m][n]            |

*(n = array length, m = string length, target = sum/goal)*

---

## 9. **Visualization**

- Draw the DP array/table and show transitions for including/excluding elements.
- For LIS, illustrate how each element looks back at previous elements.
- For subset sum, show filling the dp array and how the target sum is reached.

---

**Tip:**  
Subsequence DP is about choices: include or skip each element. Preserve order, but not contiguity. Understand the transition and initialization for your specific problem!
