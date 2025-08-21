# Dynamic Programming Pattern 10: Bitmasking DP Pattern

The **Bitmasking DP Pattern** is used for problems where you need to keep track of a set of states (such as which items/nodes have been chosen/visited) efficiently. This pattern leverages bitwise operations to represent subsets and is especially useful for combinatorial problems with small N (usually N ≤ 20).

---

## 1. **Pattern Description**

- You are given a set of items (nodes, cities, tasks, etc.), and you need to track which ones are chosen/visited.
- The state is encoded as a bitmask (an integer where each bit represents an item’s chosen/visited status).
- Classic use cases: **Traveling Salesman Problem (TSP)**, **Count All Paths Visiting All Nodes**, **Assignment Problems**, **Minimum Path Cover**.

---

## 2. **Problem Examples**

- Traveling Salesman Problem (TSP)
- Minimum Cost to Connect All Cities
- Count All Hamiltonian Paths/Cycles
- Assignment Problem (job assignment, workers to jobs)
- Shortest Path Visiting All Nodes
- Partitioning a Set Into Subsets

---

## 3. **Approach and Steps**

### Step 1: **State Representation**
- Use a bitmask integer of size N to represent the selection/visited status of each item.
  - E.g., `mask = 010101` means the 2nd, 4th, and 6th items are picked.

### Step 2: **Define DP State**
- DP state is often: `dp[pos][mask]`
  - `pos`: Current position/item/node.
  - `mask`: Bitmask representing visited/picked items.

### Step 3: **Recurrence/Transition**
- Iterate over all items.
- For each unvisited item, transition:  
  `dp[pos][mask] = min(dp[next][mask | (1 << next)] + cost[pos][next])` (for minimization)
- Base case: All items visited (`mask == (1<<N) - 1`).

### Step 4: **Optimization**
- Memoization (top-down with recursion) or Tabulation (bottom-up, rare due to state explosion).
- Bitmask is efficient for N ≤ 20 (as `2^N` states is tractable).

---

## 4. **Key Points While Coding (Java)**

- **Bitmask Creation:** Use `(1 << i)` for the i-th item.
- **Check if an item is picked:** `(mask & (1 << i)) != 0`
- **Set an item as picked:** `mask | (1 << i)`
- **Unset an item:** `mask & ~(1 << i)`
- **DP Array Size:** Usually `dp[N][1 << N]` or `dp[1 << N]` for one-dimensional.
- **Initialization:** Fill DP/memo with -1 (or Integer.MAX_VALUE for min).
- **Base Case:** All items visited (`mask == (1 << N) - 1`).
- **Recursion:** Recursively try adding each unvisited item, updating the bitmask.
- **Pruning:** For large N, prune impossible/irrelevant states.

---

## 5. **Template Code Examples (Java)**

### a) Traveling Salesman Problem (TSP) — Min Cost to Visit All Cities

```java
int tsp(int[][] cost) {
    int N = cost.length;
    int[][] memo = new int[N][1 << N];
    for (int[] row : memo) Arrays.fill(row, -1);
    return dfs(0, 1, cost, memo, N);
}

int dfs(int pos, int mask, int[][] cost, int[][] memo, int N) {
    if (mask == (1 << N) - 1) return cost[pos][0]; // Return to start
    if (memo[pos][mask] != -1) return memo[pos][mask];
    int ans = Integer.MAX_VALUE;
    for (int city = 0; city < N; city++) {
        if ((mask & (1 << city)) == 0) { // not visited
            ans = Math.min(ans, cost[pos][city] + dfs(city, mask | (1 << city), cost, memo, N));
        }
    }
    return memo[pos][mask] = ans;
}
```

### b) Assignment Problem — Min Cost to Assign N Jobs to N Workers

```java
int assignJobs(int[][] cost) {
    int N = cost.length;
    int[] memo = new int[1 << N];
    Arrays.fill(memo, -1);
    return dfs(0, 0, cost, memo, N);
}

int dfs(int worker, int mask, int[][] cost, int[] memo, int N) {
    if (worker == N) return 0;
    if (memo[mask] != -1) return memo[mask];
    int ans = Integer.MAX_VALUE;
    for (int job = 0; job < N; job++) {
        if ((mask & (1 << job)) == 0) {
            ans = Math.min(ans, cost[worker][job] + dfs(worker + 1, mask | (1 << job), cost, memo, N));
        }
    }
    return memo[mask] = ans;
}
```

---

## 6. **Key Things to Remember**

- Bitmasking works best for problems with up to 20 items.
- Each subset of items is represented by an integer mask.
- Always initialize DP/memoization arrays properly.
- Use bitwise operations for efficiency.
- For path problems, the mask tracks visited nodes.
- For assignment, the mask tracks assigned jobs/tasks.
- Watch for off-by-one errors in bit operations.

---

## 7. **Practice Problems**

1. [Traveling Salesman Problem (LeetCode 943)](https://leetcode.com/problems/find-the-shortest-superstring/)
2. [Assignment Problem (LeetCode 698)](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)
3. [Shortest Path Visiting All Nodes (LeetCode 847)](https://leetcode.com/problems/shortest-path-visiting-all-nodes/)
4. [Minimum Path Cover (GFG)](https://www.geeksforgeeks.org/minimum-number-of-paths-to-cover-all-nodes-of-a-directed-acyclic-graph/)
5. [Count All Possible Hamiltonian Cycles (GFG)](https://www.geeksforgeeks.org/counting-hamiltonian-cycles-directed-graph/)

---

## 8. **Summary Table**

| Problem Type                        | Time Complexity        | Space Complexity   | DP State         |
|------------------------------------- |-----------------------|-------------------|------------------|
| TSP (N cities)                      | O(N^2 * 2^N)          | O(N * 2^N)        | dp[pos][mask]    |
| Assignment Problem (N jobs)         | O(N^2 * 2^N)          | O(2^N)            | dp[mask]         |
| Hamiltonian Path/Count              | O(N^2 * 2^N)          | O(N * 2^N)        | dp[pos][mask]    |

---

## 9. **Visualization**

- Draw how each bit in the mask represents a picked/visited item.
- Show transitions: flipping a bit when an item is visited.
- Illustrate the recursion tree with mask changes.

---

**Tip:**  
Bitmasking DP is unbeatable for state compression in subset/assignment/path problems with small N. Master bitwise operations and visualize your mask transitions!
