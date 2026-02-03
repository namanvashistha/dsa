# Climbing Stairs

## 📋 Problem Statement

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

### Examples

**Example 1:**
```
Input: n = 2
Output: 2
Explanation: 1+1 or 2
```

**Example 2:**
```
Input: n = 3
Output: 3
Explanation: 1+1+1 or 1+2 or 2+1
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- From step n, we could have come from step n-1 or n-2
- This is Fibonacci pattern!

### Step 2: DP Recurrence
```
dp[n] = dp[n-1] + dp[n-2]
```

Base cases: dp[1] = 1, dp[2] = 2

---

## 💡 Solution

```python
def climbStairs(n: int) -> int:
    if n <= 2:
        return n
    
    prev2, prev1 = 1, 2
    
    for i in range(3, n + 1):
        curr = prev1 + prev2
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

1. **Fibonacci pattern** - Current = sum of previous two
2. **Space optimization** - Only need last 2 values
3. **Classic DP** - Foundation for harder problems

---

## 🔗 Related Problems
- House Robber
- Fibonacci Number
- Min Cost Climbing Stairs
