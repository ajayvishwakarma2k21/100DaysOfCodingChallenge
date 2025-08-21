# Dynamic Programming Pattern 8: Subarray/Substring DP Pattern

The **Subarray/Substring DP Pattern** is used for problems involving the optimal subarray or substring within a larger array or string. These problems often ask for the maximum/minimum sum, length, or count of a subarray/substring that satisfies certain conditions.

---

## 1. **Pattern Description**

- You are given an array or string and must find the best subarray or substring (contiguous elements).
- The goal is often to maximize/minimize a sum, length, or count within a subarray/substring, or to count the number of such subarrays/substrings.
- Classic examples: **Maximum Subarray Sum (Kadane's Algorithm)**, **Longest Substring Without Repeating Characters**, **Longest Substring with At Most K Distinct Characters**, **Longest Substring with All Same Letters after Replacement**.

---

## 2. **Problem Examples**

- Maximum Subarray Sum (Kadane’s Algorithm)
- Maximum Product Subarray
- Longest Substring Without Repeating Characters
- Longest Substring with At Most K Distinct Characters
- Longest Substring with All Same Letters after Replacement
- Minimum Size Subarray Sum

---

## 3. **Approach and Steps**

### Step 1: **Identify the Recurrence Relation**
- **For Maximum Subarray Sum (Kadane's Algorithm):**
  ```
  dp[i] = max(nums[i], nums[i] + dp[i-1])
  ```
- **For Longest Substring Problems (sliding window):**
  - Maintain a window with certain properties, expand and contract as needed.

### Step 2: **Choose the Method**
- **Iterative Tabulation:** Most of these problems are solved using an iterative approach with one or two variables.
- **Sliding Window:** Use two pointers to maintain a dynamic window for substring problems.
- **No Explicit DP Table:** Many subarray/substring problems can be optimized to O(1) space using clever variables instead of arrays.

---

## 4. **Key Points While Coding (Java)**

- **Initialization:** For max subarray, initialize `maxSoFar` and `maxEndingHere` (or similar) with the first element.
- **Iterate Carefully:** For sliding window, move left/right pointers based on the window’s validity.
- **Handle Edge Cases:** For empty arrays, all negative numbers, etc.
- **Space Optimization:** Most subarray/substring DP can be done in O(1) or O(n) space.
- **Hash Maps/Sets:** Useful for substring problems involving uniqueness or frequency.
- **Update Answer On-the-Fly:** Often update the answer as you scan the array/string.

---

## 5. **Template Code Examples (Java)**

### a) Maximum Subarray Sum (Kadane’s Algorithm)

```java
int maxSubArray(int[] nums) {
    int maxSoFar = nums[0], maxEndingHere = nums[0];
    for (int i = 1; i < nums.length; i++) {
        maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
        maxSoFar = Math.max(maxSoFar, maxEndingHere);
    }
    return maxSoFar;
}
```

### b) Maximum Product Subarray

```java
int maxProduct(int[] nums) {
    int maxProd = nums[0], minProd = nums[0], result = nums[0];
    for (int i = 1; i < nums.length; i++) {
        int temp = maxProd;
        maxProd = Math.max(nums[i], Math.max(maxProd * nums[i], minProd * nums[i]));
        minProd = Math.min(nums[i], Math.min(temp * nums[i], minProd * nums[i]));
        result = Math.max(result, maxProd);
    }
    return result;
}
```

### c) Longest Substring Without Repeating Characters (Sliding Window)

```java
int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int left = 0, maxLen = 0;
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        if (map.containsKey(c)) left = Math.max(left, map.get(c) + 1);
        map.put(c, right);
        maxLen = Math.max(maxLen, right - left + 1);
    }
    return maxLen;
}
```

### d) Minimum Size Subarray Sum

```java
int minSubArrayLen(int target, int[] nums) {
    int left = 0, sum = 0, minLen = Integer.MAX_VALUE;
    for (int right = 0; right < nums.length; right++) {
        sum += nums[right];
        while (sum >= target) {
            minLen = Math.min(minLen, right - left + 1);
            sum -= nums[left++];
        }
    }
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}
```

---

## 6. **Key Things to Remember**

- Many subarray/substring problems are best solved with sliding window or prefix sum, rather than classic DP tables.
- For maximum/minimum problems, update the global answer as you iterate.
- Use hash maps/sets for problems involving unique elements or frequency.
- Handle negative numbers and zeros carefully in product/sum problems.
- For window size problems, contract the window as soon as the condition is met.

---

## 7. **Practice Problems**

1. [Maximum Subarray (LeetCode)](https://leetcode.com/problems/maximum-subarray/)
2. [Maximum Product Subarray (LeetCode)](https://leetcode.com/problems/maximum-product-subarray/)
3. [Longest Substring Without Repeating Characters (LeetCode)](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
4. [Longest Substring with At Most Two Distinct Characters (LeetCode)](https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/)
5. [Minimum Size Subarray Sum (LeetCode)](https://leetcode.com/problems/minimum-size-subarray-sum/)
6. [Longest Substring with Same Letters after Replacement (LeetCode)](https://leetcode.com/problems/longest-repeating-character-replacement/)

---

## 8. **Summary Table**

| Problem Type                 | Time Complexity | Space Complexity | Common Approach      |
|------------------------------|-----------------|------------------|---------------------|
| Maximum Subarray Sum         | O(n)            | O(1)             | Kadane’s Algorithm  |
| Maximum Product Subarray     | O(n)            | O(1)             | DP with two vars    |
| Longest Unique Substring     | O(n)            | O(n)             | Sliding Window + Map|
| Minimum Size Subarray Sum    | O(n)            | O(1)             | Sliding Window      |

---

## 9. **Visualization**

- Draw the current window (left/right pointers) and how it expands/contracts.
- Plot running maximum/minimum as you iterate.
- For Kadane’s, track the running sum and global max visually.

---

**Tip:**  
Always clarify if the problem requires contiguous (subarray/substring) or non-contiguous (subsequence)! For subarray/substring, sliding window and Kadane’s are your best tools.
