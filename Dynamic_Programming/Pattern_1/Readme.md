# Dynamic Programming Pattern 1: Fibonacci / Climbing Stairs

This is the most basic and foundational DP pattern, commonly called the **Fibonacci/Climbing Stairs** pattern. Mastering this pattern will help you solve many other DP problems.

---

## 1. **Pattern Description**

- The solution to the current problem depends on solutions to one or two previous subproblems (usually the immediate previous one or two).
- The classic examples are **Fibonacci Number** and **Climbing Stairs**.

---

## 2. **Problem Examples**

- Fibonacci Number
- Climbing Stairs
- Min Cost Climbing Stairs
- Tribonacci Number
- Friends Pairing Problem

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- Recurrence relation expresses how a result for `n` depends on results for smaller values (`n-1`, `n-2`, etc.).
- Example (Fibonacci):  
  `fib(n) = fib(n-1) + fib(n-2)`
- Example (Climbing Stairs):  
  `ways(n) = ways(n-1) + ways(n-2)`

### Step 2: **Decide the Method**
- **Recursive (Brute Force):** For learning and understanding
- **Memoization (Top-Down DP):** Store results of subproblems in an array or map to avoid recomputation
- **Tabulation (Bottom-Up DP):** Build up a DP array from the base cases
- **Space Optimization:** Use two variables instead of an array if only the last two results are needed

---

## 4. **Key Points While Coding (Java)**

- **Base Cases:** Always define and handle base cases (e.g., `n = 0`, `n = 1`)
- **Array Size:** If using an array, ensure it's big enough (`dp[n+1]` for `n`)
- **Memoization Array Initialization:** Use `-1` or another marker for uncomputed values
- **Avoid Stack Overflow:** Prefer tabulation for large `n`
- **Optimize Space:** Use variables instead of an array if possible
- **Understand the Recursion Tree:** Visualize how the function calls stack up

---

## 5. **Template Code Examples (Java)**

### a) Recursive (Brute Force) - Not recommended for large n

```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

### b) Memoization (Top-Down DP)

```java
int fib(int n, int[] memo) {
    if (n <= 1) return n;
    if (memo[n] != -1) return memo[n];
    memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
    return memo[n];
}
// Usage:
int n = 10;
int[] memo = new int[n + 1];
Arrays.fill(memo, -1);
System.out.println(fib(n, memo));
```

### c) Tabulation (Bottom-Up DP)

```java
int fib(int n) {
    if (n <= 1) return n;
    int[] dp = new int[n + 1];
    dp[0] = 0;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

### d) Space Optimized

```java
int fib(int n) {
    if (n <= 1) return n;
    int prev2 = 0, prev1 = 1;
    for (int i = 2; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

---

## 6. **Typical Interview Questions**

- What is the base case?
- How do you avoid recomputation?
- Can you optimize the space complexity?
- How does the recursion tree look for small n?
- How would you prove the correctness of your recurrence relation?

---

## 7. **Practice Problems**

1. [Climbing Stairs (LeetCode)](https://leetcode.com/problems/climbing-stairs/)
2. [Fibonacci Number (LeetCode)](https://leetcode.com/problems/fibonacci-number/)
3. [Min Cost Climbing Stairs (LeetCode)](https://leetcode.com/problems/min-cost-climbing-stairs/)
4. [N-th Tribonacci Number (LeetCode)](https://leetcode.com/problems/n-th-tribonacci-number/)
5. [Friends Pairing Problem (GFG)](https://www.geeksforgeeks.org/friends-pairing-problem/)
6. [Decode Ways (LeetCode)](https://leetcode.com/problems/decode-ways/)

---

## 8. **Summary Table**

| Method         | Time Complexity | Space Complexity | Pros             | Cons               |
|----------------|----------------|------------------|------------------|--------------------|
| Recursive      | O(2^n)         | O(n)             | Simple           | Very slow, repeats |
| Memoization    | O(n)           | O(n)             | Fast, Easy       | Uses array         |
| Tabulation     | O(n)           | O(n)             | Fast             | Uses array         |
| Space Opt.     | O(n)           | O(1)             | Fast, Efficient  | Only for simple recurrences |

---

## 9. **Visualization**

- Draw recursion tree for small n.
- Show how DP array fills up in tabulation.
- Trace values of variables in space-optimized version.

---

**Tip:**  
Always start by writing the recurrence relation and base cases on paper before coding!
````
