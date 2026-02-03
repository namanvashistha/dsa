# Target Sum

## 📋 Problem Statement

You are given an integer array `nums` and an integer `target`.

You want to build an expression out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

Return the number of different expressions that you can build, which evaluates to `target`.

### Examples

**Example 1:**
```
Input: nums = [1,1,1,1,1], target = 3
Output: 5
Explanation: 
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

---

## 🧠 Thought Process

### Key Insight 💡
Let P = sum of positives, N = sum of negatives
- P + N = total
- P - N = target
- Therefore: P = (total + target) / 2

**Find number of subsets with sum P!**

---

## 💡 Solution

```python
def findTargetSumWays(nums: list[int], target: int) -> int:
    total = sum(nums)
    
    # Edge cases
    if (total + target) % 2 or abs(target) > total:
        return 0
    
    subset_sum = (total + target) // 2
    
    dp = [0] * (subset_sum + 1)
    dp[0] = 1
    
    for num in nums:
        for s in range(subset_sum, num - 1, -1):
            dp[s] += dp[s - num]
    
    return dp[subset_sum]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × sum) |
| Space | O(sum) |

---

## 🎯 Key Takeaways

1. **Transform to subset sum** - Key insight
2. **P = (total + target) / 2** - Math derivation
3. **Same as Partition Equal Subset** - Pattern recognition
4. **Backwards iteration** - 0/1 knapsack

---

## 🔗 Related Problems
- Partition Equal Subset Sum
- Last Stone Weight II
