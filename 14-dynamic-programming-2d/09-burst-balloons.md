# Burst Balloons

## 📋 Problem Statement

You are given `n` balloons indexed from `0` to `n-1`. Each balloon is painted with a number on it represented by array `nums`. You are asked to burst all the balloons.

If you burst balloon `i` you will get `nums[i-1] * nums[i] * nums[i+1]` coins. If `i-1` or `i+1` goes out of bounds, treat it as if there is a balloon with `1` painted on it.

Return the maximum coins you can collect.

### Examples

**Example 1:**
```
Input: nums = [3,1,5,8]
Output: 167
Explanation: 
Burst 1: 3×1×5 = 15
Burst 5: 3×5×8 = 120
Burst 3: 1×3×8 = 24
Burst 8: 1×8×1 = 8
Total: 167
```

---

## 🧠 Thought Process

### Key Insight 💡
**Think backwards!** Instead of which to burst first, think which to burst **last**.
- dp[i][j] = max coins from bursting all balloons between i and j
- For balloon k burst last: get nums[i] × nums[k] × nums[j]

---

## 💡 Solution

```python
def maxCoins(nums: list[int]) -> int:
    nums = [1] + nums + [1]  # Add boundary balloons
    n = len(nums)
    dp = [[0] * n for _ in range(n)]
    
    for length in range(2, n):
        for left in range(0, n - length):
            right = left + length
            
            for k in range(left + 1, right):
                # k is the last balloon burst between left and right
                coins = (nums[left] * nums[k] * nums[right] + 
                         dp[left][k] + dp[k][right])
                dp[left][right] = max(dp[left][right], coins)
    
    return dp[0][n-1]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n³) |
| Space | O(n²) |

---

## 🎯 Key Takeaways

1. **Think in reverse** - Which balloon burst LAST
2. **Add boundaries** - Virtual balloons with value 1
3. **Interval DP** - Solve by interval length
4. **dp[i][j]** - Max coins for balloons strictly between i and j

---

## 🔗 Related Problems
- Matrix Chain Multiplication
- Minimum Cost to Merge Stones
