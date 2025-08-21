# Dynamic Programming Pattern 5: Coin Change / Minimum Coin Change Pattern

The **Coin Change Pattern** is essential for solving problems where you must count or optimize the number of ways to reach a target using given denominations (coins, steps, pieces, etc.). It appears in both counting combinations and minimizing/maximizing resources.

---

## 1. **Pattern Description**

- You are given a set of denominations (coins, numbers, steps, pieces).
- You must determine the number of ways to reach a target (sum, amount, length), or the minimum/maximum number of denominations needed.
- Two main types:
  - **Count the number of ways to make the target** (combinatorics).
  - **Find the minimum (or maximum) number of denominations to reach the target** (optimization).
- Classic problems: **Coin Change**, **Coin Change II**, **Minimum Coins for Change**, **Perfect Squares**.

---

## 2. **Problem Examples**

- Coin Change
- Coin Change II (number of combinations)
- Minimum Coins to Make a Value
- Number of Ways to Make Change
- Combination Sum IV
- Perfect Squares (as a minimum coin problem)

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- **Counting Ways (Unbounded Knapsack):**
  ```
  dp[i] += dp[i - coin]   for each coin
  ```
- **Min Coins:**
  ```
  dp[i] = min(dp[i], dp[i - coin] + 1)   for each coin
  ```
- For each amount from 1 to target, consider each coin value.

### Step 2: **Decide the Method**
- **Recursive (Brute Force):** Try all combinations, very slow for large inputs.
- **Memoization (Top-Down DP):** Store results for subproblems (amount).
- **Tabulation (Bottom-Up DP):** Build a DP array from 0 to target.
- **Order of Loops:** For combinations (order doesn't matter), outer loop is coins; for permutations (order matters), outer loop is amount.

---

## 4. **Key Points While Coding (Java)**

- **DP Array Size:** Always size DP array as `dp[target + 1]`.
- **Initialization:**
  - For min coins, initialize `dp[0]=0` and the rest to `Integer.MAX_VALUE` (or a large number).
  - For counting ways, initialize `dp[0]=1`.
- **Order of Loops:** Impacts if combinations or permutations are counted.
- **Handle Overflows:** Check for `Integer.MAX_VALUE` before adding 1.
- **Return Value:** For min coins, if `dp[target]` is still `Integer.MAX_VALUE`, return -1 (not possible).
- **Duplicate Use:** Coins can be used unlimited times (unbounded).

---

## 5. **Template Code Examples (Java)**

### a) Min Coins (Coin Change)

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

### b) Number of Combinations (Coin Change II)

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

### c) Recursive with Memoization (Min Coins)

```java
int coinChange(int[] coins, int amount, int[] memo) {
    if (amount == 0) return 0;
    if (amount < 0) return -1;
    if (memo[amount] != 0) return memo[amount];
    int min = Integer.MAX_VALUE;
    for (int coin : coins) {
        int res = coinChange(coins, amount - coin, memo);
        if (res >= 0 && res < min) min = 1 + res;
    }
    memo[amount] = (min == Integer.MAX_VALUE) ? -1 : min;
    return memo[amount];
}
// Usage: int[] memo = new int[amount + 1];
```

---

## 6. **Typical Interview Questions**

- What is your DP state? (Usually amount or target)
- How do you initialize your DP array?
- What is your base case (often dp[0]=0 or dp[0]=1)?
- How does the order of loops affect the result (combinations vs permutations)?
- How do you handle cases where a solution does not exist?

---

## 7. **Practice Problems**

1. [Coin Change (LeetCode)](https://leetcode.com/problems/coin-change/)
2. [Coin Change II (LeetCode)](https://leetcode.com/problems/coin-change-ii/)
3. [Minimum Coins to Make a Value (GFG)](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)
4. [Number of Ways to Make Change (GFG)](https://www.geeksforgeeks.org/coin-change-dp-7/)
5. [Combination Sum IV (LeetCode)](https://leetcode.com/problems/combination-sum-iv/)
6. [Perfect Squares (LeetCode)](https://leetcode.com/problems/perfect-squares/)

---

## 8. **Summary Table**

| Problem Type        | Time Complexity | Space Complexity | DP State   | Initialization |
|---------------------|-----------------|------------------|------------|----------------|
| Min Coins           | O(n * amount)   | O(amount)        | dp[amount] | dp[0]=0, rest MAX|
| Count Combinations  | O(n * amount)   | O(amount)        | dp[amount] | dp[0]=1        |

*(n = number of coins, amount = target value)*

---

## 9. **Visualization**

- Draw the DP array for a small example.
- Trace how each coin updates the DP array.
- Show the difference between combinations (order doesn’t matter) and permutations (order matters).

---

**Tip:**  
Always clarify if the problem asks for number of ways (combinations) or minimum coins, and choose the correct DP state and initialization!
