# Interleaving String

## 📋 Problem Statement

Given strings `s1`, `s2`, and `s3`, find whether `s3` is formed by an interleaving of `s1` and `s2`.

An interleaving is formed by taking some characters from `s1` and `s2` alternately while preserving their relative order.

### Examples

**Example 1:**
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
```

---

## 💡 Solution

```python
def isInterleave(s1: str, s2: str, s3: str) -> bool:
    m, n = len(s1), len(s2)
    
    if m + n != len(s3):
        return False
    
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True
    
    # Fill first row
    for j in range(1, n + 1):
        dp[0][j] = dp[0][j-1] and s2[j-1] == s3[j-1]
    
    # Fill first column
    for i in range(1, m + 1):
        dp[i][0] = dp[i-1][0] and s1[i-1] == s3[i-1]
    
    # Fill rest
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            dp[i][j] = ((dp[i-1][j] and s1[i-1] == s3[i+j-1]) or
                        (dp[i][j-1] and s2[j-1] == s3[i+j-1]))
    
    return dp[m][n]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **2D DP** - Track positions in both strings
2. **dp[i][j]** - Can s1[0:i] and s2[0:j] form s3[0:i+j]
3. **Two choices** - Take from s1 or s2
4. **Length check first** - Quick validation

---

## 🔗 Related Problems
- Edit Distance
- Distinct Subsequences
