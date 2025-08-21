# Dynamic Programming Pattern 2: 0/1 Knapsack

The **0/1 Knapsack Pattern** is one of the most important and versatile DP patterns. Many subset, selection, and optimization problems can be solved using this approach. Mastering this pattern is crucial for interviews and competitive programming.

---

## 1. **Pattern Description**

- You are given a set of items, each with a certain value and/or weight.
- You must decide whether to **include or exclude** each item to achieve an optimal result (maximize/minimize value, reach a target sum, etc).
- **"0/1"** means each item can be picked **at most once** (not unlimited times).
- The classic example is the **0/1 Knapsack Problem**.

---

## 2. **Problem Examples**

- 0/1 Knapsack
- Subset Sum
- Partition Equal Subset Sum
- Target Sum
- Count of Subset Sums
- Last Stone Weight II

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- For each item (index `i`), you have two choices:
  - **Include** the item (if it fits): add its value and reduce the capacity accordingly.
  - **Exclude** the item: move to the next item.
- Example (Knapsack):
  ```
  dp[i][w] = max(
    value[i] + dp[i-1][w - weight[i]], // include item
    dp[i-1][w]                         // exclude item
  )
  ```

### Step 2: **Decide the Method**
- **Recursive (Brute Force):** Try all combinations by including/excluding each item.
- **Memoization (Top-Down DP):** Store results for subproblems (by item index and remaining capacity).
- **Tabulation (Bottom-Up DP):** Fill a DP table iteratively.
- **Space Optimization:** Use a 1D array if possible.

---

## 4. **Key Points While Coding (Java)**

- **DP Table Dimensions:** Most problems use `dp[index][capacity]` or `dp[index][sum]`.
- **Base Cases:** Usually when `index == 0` or `capacity == 0`.
- **Initialization:** Carefully initialize base cases in the DP table.
- **Memoization Array:** Use `-1` for uncomputed values.
- **Avoid Stack Overflow:** Prefer tabulation for large inputs.
- **Input Constraints:** Watch out for large capacities/target sums (optimize space/time).
- **Traceback:** For some problems, you may be asked to find the actual items used.

---

## 5. **Template Code Examples (Java)**

### a) Recursive (Brute Force) — Not for large inputs

```java
int knapsack(int[] weight, int[] value, int n, int capacity) {
    if (n == 0 || capacity == 0) return 0;
    if (weight[n-1] > capacity)
        return knapsack(weight, value, n-1, capacity);
    else
        return Math.max(
            value[n-1] + knapsack(weight, value, n-1, capacity - weight[n-1]),
            knapsack(weight, value, n-1, capacity)
        );
}
```

### b) Memoization (Top-Down DP)

```java
int knapsack(int[] weight, int[] value, int n, int capacity, int[][] memo) {
    if (n == 0 || capacity == 0) return 0;
    if (memo[n][capacity] != -1) return memo[n][capacity];
    if (weight[n-1] > capacity)
        memo[n][capacity] = knapsack(weight, value, n-1, capacity, memo);
    else
        memo[n][capacity] = Math.max(
            value[n-1] + knapsack(weight, value, n-1, capacity - weight[n-1], memo),
            knapsack(weight, value, n-1, capacity, memo)
        );
    return memo[n][capacity];
}
// Usage:
int[][] memo = new int[n+1][capacity+1];
for (int[] row : memo) Arrays.fill(row, -1);
```

### c) Tabulation (Bottom-Up DP)

```java
int knapsack(int[] weight, int[] value, int n, int capacity) {
    int[][] dp = new int[n+1][capacity+1];
    for (int i = 0; i <= n; i++) {
        for (int w = 0; w <= capacity; w++) {
            if (i == 0 || w == 0)
                dp[i][w] = 0;
            else if (weight[i-1] <= w)
                dp[i][w] = Math.max(value[i-1] + dp[i-1][w - weight[i-1]], dp[i-1][w]);
            else
                dp[i][w] = dp[i-1][w];
        }
    }
    return dp[n][capacity];
}
```

### d) Space Optimized

```java
int knapsack(int[] weight, int[] value, int n, int capacity) {
    int[] dp = new int[capacity + 1];
    for (int i = 0; i < n; i++) {
        for (int w = capacity; w >= weight[i]; w--) {
            dp[w] = Math.max(dp[w], value[i] + dp[w - weight[i]]);
        }
    }
    return dp[capacity];
}
```

---

## 6. **Typical Interview Questions**

- How do you derive the recurrence relation?
- What are your base cases and how do you initialize the DP table?
- Can you optimize the space complexity?
- How do you reconstruct the subset/items chosen?
- How does the time/space complexity scale with input size?

---

## 7. **Practice Problems**

1. [0/1 Knapsack Problem (GFG)](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)
2. [Subset Sum Problem (GFG)](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)
3. [Partition Equal Subset Sum (LeetCode)](https://leetcode.com/problems/partition-equal-subset-sum/)
4. [Target Sum (LeetCode)](https://leetcode.com/problems/target-sum/)
5. [Count of Subset Sum (GFG)](https://www.geeksforgeeks.org/count-of-subsets-with-sum-equal-to-x/)
6. [Last Stone Weight II (LeetCode)](https://leetcode.com/problems/last-stone-weight-ii/)

---

## 8. **Summary Table**

| Method         | Time Complexity   | Space Complexity | Pros           | Cons                 |
|----------------|------------------|------------------|----------------|----------------------|
| Recursive      | O(2^n)           | O(n)             | Simple         | Very slow, repeats   |
| Memoization    | O(n * cap)       | O(n * cap)       | Fast, Easy     | Uses DP array        |
| Tabulation     | O(n * cap)       | O(n * cap)       | Fast           | Uses DP array        |
| Space Opt.     | O(n * cap)       | O(cap)           | Efficient      | May be tricky        |

*(n = number of items, cap = capacity or target sum)*

---

## 9. **Visualization**

- Draw the decision tree for small inputs (include/exclude each item).
- Show how the DP table (2D array) fills up in tabulation.
- Trace the values in the 1D array for space-optimized solution.

---

**Tip:**  
Always write the recurrence relation and draw a table for a few small cases before coding!
