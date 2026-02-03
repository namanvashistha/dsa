# Distinct Subsequences

## 📋 Problem Statement

Given two strings `s` and `t`, return the number of distinct subsequences of `s` which equals `t`.

### Examples

**Example 1:**
```
Input: s = "rabbbit", t = "rabbit"
Output: 3
```

---

## 💡 Solution

```python
def numDistinct(s: str, t: str) -> int:
    m, n = len(s), len(t)
    
    # dp[j] = ways to form t[0:j]
    dp = [0] * (n + 1)
    dp[0] = 1  # Empty string match
    
    for i in range(1, m + 1):
        # Iterate backwards to avoid using updated values
        for j in range(min(i, n), 0, -1):
            if s[i-1] == t[j-1]:
                dp[j] += dp[j-1]
    
    return dp[n]
```

---

## 📊 Recurrence

```
if s[i] == t[j]:
    dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
else:
    dp[i][j] = dp[i-1][j]
```

- Match: use char OR skip char in s
- No match: must skip char in s

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Two choices on match** - Use or skip
2. **One choice on mismatch** - Skip
3. **Space optimized** - Iterate backwards
4. **dp[0] = 1** - Empty subsequence always matches

---

## 🔗 Related Problems
- Edit Distance
- Longest Common Subsequence
