# House Robber

## 📋 Problem Statement

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. Adjacent houses have security systems connected, so **robbing two adjacent houses will alert the police**.

Given an integer array `nums` representing money in each house, return the maximum amount of money you can rob without alerting police.

### Examples

**Example 1:**
```
Input: nums = [1,2,3,1]
Output: 4
Explanation: Rob house 1 ($1) and house 3 ($3) = $4
```

**Example 2:**
```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 ($2) + house 3 ($9) + house 5 ($1) = $12
```

---

## 🧠 Thought Process

### Step 1: DP Choice at Each House
At house i:
- **Rob:** Take nums[i] + best from 2 houses before
- **Skip:** Take best from previous house

```
dp[i] = max(dp[i-1], dp[i-2] + nums[i])
```

---

## 💡 Solution

```python
def rob(nums: list[int]) -> int:
    if len(nums) == 1:
        return nums[0]
    
    prev2, prev1 = 0, 0
    
    for num in nums:
        curr = max(prev1, prev2 + num)
        prev2, prev1 = prev1, curr
    
    return prev1
```

---

## 🔍 Detailed Walkthrough

```
nums = [2, 7, 9, 3, 1]

i=0 (num=2): curr = max(0, 0+2) = 2
             prev2=0, prev1=2

i=1 (num=7): curr = max(2, 0+7) = 7
             prev2=2, prev1=7

i=2 (num=9): curr = max(7, 2+9) = 11
             prev2=7, prev1=11

i=3 (num=3): curr = max(11, 7+3) = 11
             prev2=11, prev1=11

i=4 (num=1): curr = max(11, 11+1) = 12
             prev2=11, prev1=12

Result: 12 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Rob or skip** - Binary choice at each position
2. **Can't take adjacent** - Look 2 back when robbing
3. **Space optimization** - Only need prev2 values
4. **Pattern: max(include, exclude)**

---

## 🔗 Related Problems
- House Robber II (circular)
- House Robber III (tree)
- Delete and Earn
