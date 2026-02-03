# 🎯🎯 2-D Dynamic Programming - NeetCode 150

> 11 problems | Master grid DP and multi-dimensional state transitions

---

## 1️⃣ Unique Paths ⭐⭐ Medium
**The Trick:** Sum of paths from top and left
- `dp[i][j] = dp[i-1][j] + dp[i][j-1]`
- Can only move right or down
- **Remember:** Current = top + left

---

## 2️⃣ Longest Common Subsequence ⭐⭐ Medium
**The Trick:** Match or skip characters
- If `s1[i] == s2[j]`: `dp[i][j] = dp[i-1][j-1] + 1`
- Else: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`
- **Remember:** Match = diagonal + 1, else max of top/left

---

## 3️⃣ Best Time to Buy and Sell Stock with Cooldown ⭐⭐ Medium
**The Trick:** Three states (hold, sold, rest)
- State machine: hold ↔ sold → rest → hold
- Track max profit in each state
- **Remember:** Cooldown = can't buy immediately after sell

**States:**
- `hold[i]` = max profit if holding stock at day i
- `sold[i]` = max profit if just sold at day i
- `rest[i]` = max profit if resting at day i

---

## 4️⃣ Coin Change II ⭐⭐ Medium
**The Trick:** Count combinations (unbounded knapsack)
- `dp[i][amount]` = ways using first i coins
- Use coin: `dp[i][amount-coin]`
- Skip coin: `dp[i-1][amount]`
- **Remember:** Combinations, not permutations (order doesn't matter)

**1D optimization:** `dp[amount]`, iterate coins outside

---

## 5️⃣ Target Sum ⭐⭐ Medium
**The Trick:** Convert to subset sum problem
- Add + or - to each number to reach target
- Math: `(sum + target) / 2` = sum of positive subset
- Count subsets with this sum
- **Remember:** Subset sum DP with specific target

---

## 6️⃣ Interleaving String ⭐⭐ Medium
**The Trick:** Two pointers in s1 and s2
- `dp[i][j]` = can form s3[0:i+j] from s1[0:i] and s2[0:j]
- If `s1[i] == s3[i+j]`: check `dp[i-1][j]`
- If `s2[j] == s3[i+j]`: check `dp[i][j-1]`
- **Remember:** Check if can extend from either string

---

## 7️⃣ Longest Increasing Path in Matrix ⭐⭐⭐ Hard
**The Trick:** DFS + memoization
- DFS from each cell, go to larger neighbors
- Memoize result for each cell
- `dp[i][j]` = longest path starting from (i,j)
- **Remember:** DFS with memo, directed graph (increasing only)

---

## 8️⃣ Distinct Subsequences ⭐⭐⭐ Hard
**The Trick:** Count ways to form t from s
- If `s[i] == t[j]`: use it or skip it
  - `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]`
- Else: skip `s[i]`
  - `dp[i][j] = dp[i-1][j]`
- **Remember:** Match = use + skip, no match = skip only

---

## 9️⃣ Edit Distance ⭐⭐⭐ Hard
**The Trick:** Min operations (insert, delete, replace)
- If chars match: `dp[i][j] = dp[i-1][j-1]`
- Else: `dp[i][j] = 1 + min(insert, delete, replace)`
  - Insert: `dp[i][j-1]`
  - Delete: `dp[i-1][j]`
  - Replace: `dp[i-1][j-1]`
- **Remember:** Match = free, else 1 + min of 3 ops

---

## 🔟 Burst Balloons ⭐⭐⭐ Hard
**The Trick:** Think backwards - which balloon to burst last?
- `dp[i][j]` = max coins from bursting balloons i to j
- For each k in [i,j], burst k last
- Coins = `nums[i-1] × nums[k] × nums[j+1] + dp[i][k-1] + dp[k+1][j]`
- **Remember:** Last balloon to burst, not first

---

## 1️⃣1️⃣ Regular Expression Matching ⭐⭐⭐ Hard
**The Trick:** Handle '.' and '*' cases
- '.' matches any single char
- '*' matches zero or more of previous char
- `dp[i][j]` = does s[0:i] match p[0:j]
- **Remember:** '*' can match 0 times or 1+ times

**Cases:**
- If `p[j] == '*'`: try 0 match `dp[i][j-2]` or 1+ match
- If chars match or '.': `dp[i][j] = dp[i-1][j-1]`

---

## 🎯 Pattern Recognition

**2D DP Dimensions:**
- **Grid problems:** `dp[row][col]`
- **Two strings:** `dp[i][j]` for s1[0:i] and s2[0:j]
- **Sequence + constraint:** `dp[i][state]`

**Common 2D Patterns:**

1. **Grid traversal:**
   - Unique paths: sum from top and left
   - Min path sum: min of top and left + current

2. **String matching:**
   - LCS: match chars or skip
   - Edit distance: min of insert/delete/replace
   - Pattern matching: handle special chars

3. **Knapsack variants:**
   - `dp[i][capacity/sum]`
   - Include item or skip

4. **Range DP:**
   - `dp[i][j]` = answer for range [i, j]
   - Burst balloons, palindrome partitioning

**2D DP Template:**
```python
# Define meaning of dp[i][j]
dp = [[base] * (n + 1) for _ in range(m + 1)]

# Initialize base cases
for i in range(m + 1):
    dp[i][0] = ...
for j in range(n + 1):
    dp[0][j] = ...

# Fill table
for i in range(1, m + 1):
    for j in range(1, n + 1):
        # Transition based on problem
        dp[i][j] = function(dp[i-1][j], dp[i][j-1], ...)

return dp[m][n]
```

**String DP Common Pattern:**
```python
# s1[0:i] vs s2[0:j]
for i in range(1, len(s1) + 1):
    for j in range(1, len(s2) + 1):
        if s1[i-1] == s2[j-1]:
            dp[i][j] = dp[i-1][j-1] + something
        else:
            dp[i][j] = best(dp[i-1][j], dp[i][j-1])
```

**Space Optimization:**
- If only need previous row: use 1D array
- Rolling array: `dp[i%2][j]`
- For string problems: often can use O(min(m,n))

**Range DP Pattern:**
```python
# Fill by increasing length
for length in range(2, n + 1):
    for i in range(n - length + 1):
        j = i + length - 1
        # Try all split points k in [i, j]
        for k in range(i, j + 1):
            dp[i][j] = best(dp[i][j], dp[i][k] + dp[k+1][j] + cost)
```

**Time Complexity:**
- Grid: O(m × n)
- String matching: O(m × n)
- Range DP: O(n³) - three nested loops

**Common Mistakes:**
- Off-by-one in string indexing (i vs i-1)
- Wrong base cases (empty string scenarios)
- Not considering all transitions
- Wrong dimensions of dp array
- Confusing dp[i][j] meaning

**Key Insights:**
- **Grid:** Usually sum/min/max from neighbors
- **Strings:** Compare characters, match or skip
- **Knapsack:** Include or exclude item
- **Range DP:** Try all split points
- Draw the DP table for small examples!
- Base cases: empty string, zero capacity, single cell

**Pattern Recognition Tips:**
- Two strings → probably 2D string DP
- Grid movement → 2D grid DP
- Items + capacity → knapsack variant
- Range/interval → range DP
- State machine → state-based DP

**Debugging:**
1. Print dp table for small input
2. Verify base cases
3. Check transition logic
4. Ensure indices correct (0-indexed vs 1-indexed)
