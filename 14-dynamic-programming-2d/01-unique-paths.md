# Unique Paths

## 📋 Problem Statement

There is a robot on an `m x n` grid. The robot is initially at the top-left corner and tries to move to the bottom-right corner. It can only move either down or right at any point.

Return the number of possible unique paths.

### Examples

**Example 1:**
```
Input: m = 3, n = 7
Output: 28
```

---

## 💡 Solution: DP

```python
def uniquePaths(m: int, n: int) -> int:
    dp = [1] * n  # First row all 1s
    
    for _ in range(1, m):
        for j in range(1, n):
            dp[j] += dp[j-1]
    
    return dp[-1]
```

## 💡 Solution: Math

```python
from math import comb

def uniquePaths(m: int, n: int) -> int:
    # Need m-1 downs and n-1 rights
    # Choose positions for m-1 downs out of m+n-2 moves
    return comb(m + n - 2, m - 1)
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| DP | O(m×n) | O(n) |
| Math | O(min(m,n)) | O(1) |

---

## 🎯 Key Takeaways

1. **dp[i][j] = dp[i-1][j] + dp[i][j-1]**
2. **First row/col = 1** - Only one way
3. **Space optimization** - Single row
4. **Math solution** - Combinatorics

---

## 🔗 Related Problems
- Unique Paths II (obstacles)
- Minimum Path Sum
