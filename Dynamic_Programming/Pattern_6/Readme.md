# Dynamic Programming Pattern 6: Unbounded Knapsack

The **Unbounded Knapsack Pattern** is used for problems where you can use each item an unlimited number of times (not just once, as in 0/1 Knapsack). This pattern is fundamental for many optimization and combinatorial problems in dynamic programming.

---

## 1. **Pattern Description**

- You are given a set of items, each with a value and/or weight (or cost, length, etc.).
- **You can use each item as many times as you want** (unlimited supply).
- The goal is usually to maximize or minimize some objective (total value, length, cost, etc.) or to count the number of ways to reach a target.
- Classic example: **Unbounded Knapsack**.

---

## 2. **Problem Examples**

- Unbounded Knapsack
- Rod Cutting
- Coin Change (Number of Ways)
- Minimum Number of Coins for Change
- Integer Break

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- For each item, at every step, you have two choices:
  - **Include** the item (and stay at the same index because items are unlimited).
  - **Exclude** the item (move to the next item).
- Example (Unbounded Knapsack):
  ```
  dp[i][w] = max(
    value[i] + dp[i][w - weight[i]], // include item (stay at i)
    dp[i-1][w]                       // exclude item
  )
  ```
- For 1D DP (space optimized), iterate outer loop over capacity and inner over items.

### Step 2: **Choose Method**
- **Recursive (Brute Force):** Try all combinations, slow for large input.
- **Memoization (Top-Down DP):** Use a 2D (or 1D) array for (index, remaining capacity).
- **Tabulation (Bottom-Up DP):** Build a DP table, usually 1D for space efficiency.

---

## 4. **Key Points While Coding (Java)**

- **DP Table:** For tabulation, 1D array `dp[capacity + 1]` is common.
- **Initialization:**
  - For maximization, initialize `dp[0]=0` and the rest to `0`.
  - For minimization, initialize `dp[0]=0` and the rest to a large number.
- **Order of Loops:** Outer loop over capacity, inner loop over items for optimality.
- **Unlimited Supply:** When including an item, **do not move to the next item** (stay at current index).
- **Base Cases:** Usually `dp[0]=0` (no capacity/target requires zero cost/ways).
- **Edge Cases:** Handle cases when a solution is not possible.

---

## 5. **Template Code Examples (Java)**

### a) Tabulation (Bottom-Up) — Max Value (Unbounded Knapsack)

```java
int unboundedKnapsack(int[] weight, int[] value, int n, int capacity) {
    int[] dp = new int[capacity + 1];
    for (int w = 0; w <= capacity; w++) {
        for (int i = 0; i < n; i++) {
            if (weight[i] <= w)
                dp[w] = Math.max(dp[w], value[i] + dp[w - weight[i]]);
        }
    }
    return dp[capacity];
}
```

### b) Tabulation — Counting Ways (Coin Change II)

```java
int change(int amount, int[] coins) {
    int[] dp = new int[amount + 1];
    dp[0] = 1;
    for (int coin : coins) {
        for (int i = coin; i <= amount; i++) {
            dp[i] += dp[i - coin];
        }
    }
    return dp[amount];
}
```

### c) Tabulation — Min Number of Coins

```java
int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1];
    Arrays.fill(dp, amount + 1);
    dp[0] = 0;
    for (int i = 1; i <= amount; i++) {
        for (int coin : coins) {
            if (i - coin >= 0)
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
        }
    }
    return dp[amount] > amount ? -1 : dp[amount];
}
```

### d) Rod Cutting

```java
int rodCutting(int[] prices, int n) {
    int[] dp = new int[n + 1];
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= i; j++) {
            dp[i] = Math.max(dp[i], prices[j - 1] + dp[i - j]);
        }
    }
    return dp[n];
}
```

---

## 6. **Typical Interview Questions**

- How is this different from 0/1 Knapsack?
- How do you ensure unlimited usage of items in your code?
- What is your DP state and initialization?
- How do you optimize your solution for time/space?
- What is the order of your loops, and why does it matter?

---

## 7. **Practice Problems**

1. [Unbounded Knapsack (GFG)](https://www.geeksforgeeks.org/unbounded-knapsack-repetition-items-allowed/)
2. [Rod Cutting (LeetCode)](https://leetcode.com/problems/minimum-cost-to-cut-a-stick/)
3. [Coin Change II (LeetCode)](https://leetcode.com/problems/coin-change-ii/)
4. [Integer Break (LeetCode)](https://leetcode.com/problems/integer-break/)
5. [Word Break (LeetCode)](https://leetcode.com/problems/word-break/)
6. [Minimum Coins to Make a Value (GFG)](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)

---

## 8. **Summary Table**

| Problem Type        | Time Complexity   | Space Complexity | DP State             |
|---------------------|------------------|------------------|----------------------|
| Max Value           | O(n * cap)       | O(cap)           | dp[cap]              |
| Count Ways          | O(n * amount)    | O(amount)        | dp[amount]           |
| Min Coins           | O(n * amount)    | O(amount)        | dp[amount]           |

*(n = number of items/coins, cap/amount = capacity/target value)*

---

## 9. **Visualization**

- Draw the DP array for small examples.
- Show how each item/coin updates the DP array for each capacity/amount.
- Trace the difference in loop order and its effect on unlimited usage.

---

**Tip:**  
When items are unlimited, after including one, **stay at the same index** and keep considering it. Always clarify if you can reuse items or not!
