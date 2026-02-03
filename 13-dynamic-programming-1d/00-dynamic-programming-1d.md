# 🎯 1-D Dynamic Programming - NeetCode 150

> 12 problems | Master linear DP patterns and state transitions

---

## 1️⃣ Climbing Stairs ⭐ Easy
**The Trick:** Fibonacci pattern
- Ways to reach step n = ways(n-1) + ways(n-2)
- Base: step 0 = 1, step 1 = 1
- **Remember:** `dp[i] = dp[i-1] + dp[i-2]`

---

## 2️⃣ Min Cost Climbing Stairs ⭐ Easy
**The Trick:** Choose cheaper of previous two steps
- `dp[i] = cost[i] + min(dp[i-1], dp[i-2])`
- Can start from step 0 or 1
- **Remember:** Add current cost + min of previous

---

## 3️⃣ House Robber ⭐⭐ Medium
**The Trick:** Rob current or skip (can't rob adjacent)
- `dp[i] = max(rob current + dp[i-2], skip = dp[i-1])`
- **Remember:** Max of (current + i-2) vs (i-1)

**Optimized:** Only need last two values
```python
prev2, prev1 = 0, 0
for num in nums:
    current = max(prev1, prev2 + num)
    prev2, prev1 = prev1, current
```

---

## 4️⃣ House Robber II ⭐⭐ Medium
**The Trick:** Houses in circle → two cases
- Case 1: Rob house 0, can't rob last
- Case 2: Skip house 0, can rob last
- Run House Robber I on both ranges
- **Remember:** Circle = two separate linear problems

---

## 5️⃣ Longest Palindromic Substring ⭐⭐ Medium
**The Trick:** Expand around center
- For each center (single char or pair)
- Expand while characters match
- Track longest found
- **Remember:** 2n-1 centers (n single + n-1 pairs)

**Alternative:** DP with `dp[i][j]` = is s[i:j+1] palindrome

---

## 6️⃣ Palindromic Substrings ⭐⭐ Medium
**The Trick:** Count while expanding around centers
- Same as above but count instead of track longest
- Each expansion = valid palindrome
- **Remember:** Count all, not just longest

---

## 7️⃣ Decode Ways ⭐⭐ Medium
**The Trick:** Count ways to decode string
- `dp[i]` = ways to decode s[0:i]
- Single digit (1-9): add `dp[i-1]`
- Two digits (10-26): add `dp[i-2]`
- **Remember:** Consider last 1 and last 2 digits

---

## 8️⃣ Coin Change ⭐⭐ Medium
**The Trick:** Min coins for each amount
- `dp[i]` = min coins to make amount i
- For each coin: `dp[i] = min(dp[i], dp[i-coin] + 1)`
- **Remember:** Try each coin, take minimum

---

## 9️⃣ Maximum Product Subarray ⭐⭐ Medium
**The Trick:** Track both max and min (negatives!)
- Negative × negative = positive
- Track max_prod and min_prod
- Update both each step
- **Remember:** Min can become max with negative

```python
max_prod = min_prod = result = nums[0]
for num in nums[1:]:
    if num < 0:
        max_prod, min_prod = min_prod, max_prod
    max_prod = max(num, max_prod * num)
    min_prod = min(num, min_prod * num)
    result = max(result, max_prod)
```

---

## 🔟 Word Break ⭐⭐ Medium
**The Trick:** DP with dictionary lookup
- `dp[i]` = can break s[0:i]
- For each i, try all words ending at i
- If `s[j:i]` in dict and `dp[j]` true → `dp[i]` true
- **Remember:** Check all possible last words

---

## 1️⃣1️⃣ Longest Increasing Subsequence ⭐⭐ Medium
**The Trick:** DP counting LIS ending at each index
- `dp[i]` = length of LIS ending at i
- For each j < i: if `nums[j] < nums[i]`, consider `dp[j] + 1`
- **Remember:** O(n²) DP or O(n log n) binary search

**Optimized:** Maintain sorted array of LIS candidates

---

## 1️⃣2️⃣ Partition Equal Subset Sum ⭐⭐ Medium
**The Trick:** Subset sum = half of total (0/1 knapsack)
- Target = sum(nums) / 2
- Can we make subset with target sum?
- `dp[s]` = can make sum s
- **Remember:** If odd total, impossible

---

## 🎯 Pattern Recognition

**DP Patterns:**

1. **Linear DP:** Current depends on previous
   - Climbing stairs, house robber
   - `dp[i]` depends on `dp[i-1]`, `dp[i-2]`, etc.

2. **Two Variables:** Track multiple states
   - Max and min (product subarray)
   - Rob or skip (house robber)

3. **Subset/Knapsack:** Can we make sum/weight?
   - Coin change, partition
   - `dp[sum]` or `dp[i][sum]`

4. **String DP:** Expand or match patterns
   - Palindrome, word break
   - Check substrings

**DP Template:**
```python
# 1. Define dp array and meaning
dp = [base_case] * (n + 1)

# 2. Initialize base cases
dp[0] = ...

# 3. Fill dp array
for i in range(1, n + 1):
    # Transition from previous states
    dp[i] = function(dp[i-1], dp[i-2], ...)

# 4. Return answer
return dp[n]
```

**Space Optimization:**
- If only need last k values → use k variables
- House Robber: only need prev1, prev2

**Bottom-up vs Top-down:**
- **Bottom-up (Tabulation):** Iterative, fill table
- **Top-down (Memoization):** Recursive with cache

**Memoization Template:**
```python
@cache  # or use memo dict
def dp(i, ...):
    if base_case:
        return ...
    
    # Try all choices, return best
    return best(dp(next_state1), dp(next_state2))
```

**Common Patterns:**

- **Fibonacci-like:** `dp[i] = dp[i-1] + dp[i-2]`
- **Min/Max choice:** `dp[i] = min/max(choice1, choice2, ...)`
- **Sum accumulation:** `dp[i] = dp[i-1] + ...`
- **Boolean (possible?):** `dp[i] = dp[j] and condition`

**Time Complexity:**
- Usually O(n) or O(n²)
- With choices at each step: O(n × choices)

**Common Mistakes:**
- Wrong base cases
- Off-by-one errors in indices
- Not considering all previous states
- Forgetting to track min AND max (product problems)
- Not checking for impossible cases first

**Key Insights:**
- DP = optimal substructure + overlapping subproblems
- Define state clearly: "dp[i] means..."
- Think: "What do I need to know to solve dp[i]?"
- Negative numbers → track min AND max
- Circle/cycle → break into linear cases
- Can optimize space if only need recent values

**When to use DP:**
- Optimal solution (min/max)
- Count number of ways
- Yes/no (is it possible?)
- "Find all", "find longest", "find minimum"
