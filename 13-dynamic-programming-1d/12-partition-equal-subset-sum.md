# Partition Equal Subset Sum

## 📋 Problem Statement

Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal.

### Examples

**Example 1:**
```
Input: nums = [1,5,11,5]
Output: true
Explanation: [1,5,5] and [11]
```

---

## 🧠 Thought Process

### Key Insight 💡
1. Total sum must be even
2. Find subset with sum = total/2
3. This is the **0/1 Knapsack** problem!

---

## 💡 Solution

```python
def canPartition(nums: list[int]) -> bool:
    total = sum(nums)
    
    if total % 2:
        return False
    
    target = total // 2
    dp = {0}  # Achievable sums
    
    for num in nums:
        new_dp = set()
        for s in dp:
            if s + num == target:
                return True
            new_dp.add(s + num)
        dp.update(new_dp)
    
    return target in dp
```

## 💡 Solution: Boolean DP

```python
def canPartition(nums: list[int]) -> bool:
    total = sum(nums)
    
    if total % 2:
        return False
    
    target = total // 2
    dp = [False] * (target + 1)
    dp[0] = True
    
    for num in nums:
        for s in range(target, num - 1, -1):
            dp[s] = dp[s] or dp[s - num]
    
    return dp[target]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × sum) |
| Space | O(sum) |

---

## 🎯 Key Takeaways

1. **Even sum required** - Otherwise impossible
2. **Find target = sum/2** - Subset sum problem
3. **Iterate backwards** - Prevent reusing elements
4. **0/1 Knapsack variant**

---

## 🔗 Related Problems
- Target Sum
- Last Stone Weight II
