# House Robber II

## 📋 Problem Statement

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle**. Adjacent houses have security systems connected so two adjacent houses cannot be robbed on the same night.

Return the maximum amount you can rob without alerting the police.

### Examples

**Example 1:**
```
Input: nums = [2,3,2]
Output: 3
Explanation: Cannot rob 1st and 3rd (adjacent in circle).
```

---

## 🧠 Thought Process

### Key Insight 💡
**Circle = first and last are adjacent!**
- Either skip first house OR skip last house
- Run House Robber I twice
- Take maximum

---

## 💡 Solution

```python
def rob(nums: list[int]) -> int:
    if len(nums) == 1:
        return nums[0]
    
    def rob_linear(houses):
        prev2, prev1 = 0, 0
        for h in houses:
            curr = max(prev1, prev2 + h)
            prev2, prev1 = prev1, curr
        return prev1
    
    return max(rob_linear(nums[:-1]), rob_linear(nums[1:]))
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Break the circle** - Two linear cases
2. **Skip first OR last** - Avoids circular adjacency
3. **Reuse House Robber I** - Core logic same
4. **Take max of both** - Optimal answer

---

## 🔗 Related Problems
- House Robber
- House Robber III (Tree)
