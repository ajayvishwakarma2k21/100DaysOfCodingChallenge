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
```python
for i in items:
    for w in range(capacity, weight[i]-1, -1):
        dp[w] = max(dp[w], dp[w - weight[i]] + value[i])
