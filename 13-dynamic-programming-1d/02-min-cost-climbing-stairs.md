# Min Cost Climbing Stairs

## 📋 Problem Statement

You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from step 0 or step 1.

Return the minimum cost to reach the top of the floor.

### Examples

**Example 1:**
```
Input: cost = [10,15,20]
Output: 15
Explanation: Start at index 1, pay 15, climb 2 steps to reach top.
```

**Example 2:**
```
Input: cost = [1,100,1,1,1,100,1,1,100,1]
Output: 6
```

---

## 💡 Solution

```python
def minCostClimbingStairs(cost: list[int]) -> int:
    n = len(cost)
    
    # Bottom-up DP
    prev2, prev1 = 0, 0
    
    for i in range(2, n + 1):
        curr = min(prev1 + cost[i-1], prev2 + cost[i-2])
        prev2, prev1 = prev1, curr
    
    return prev1
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **dp[i] = min cost to reach step i**
2. **Can come from i-1 or i-2**
3. **O(1) space** - Only need last two values
4. **Top = step n** - Beyond last step

---

## 🔗 Related Problems
- Climbing Stairs
- House Robber
