# Regular Expression Matching

## 📋 Problem Statement

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `.` and `*`:
- `.` Matches any single character.
- `*` Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

### Examples

**Example 1:**
```
Input: s = "aa", p = "a"
Output: false
```

**Example 2:**
```
Input: s = "aa", p = "a*"
Output: true
```

---

## 💡 Solution

```python
def isMatch(s: str, p: str) -> bool:
    m, n = len(s), len(p)
    dp = [[False] * (n + 1) for _ in range(m + 1)]
    dp[0][0] = True
    
    # Handle patterns like a*, a*b*, etc. that can match empty string
    for j in range(2, n + 1):
        if p[j-1] == '*':
            dp[0][j] = dp[0][j-2]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if p[j-1] == '*':
                # Zero occurrences OR one+ occurrences
                dp[i][j] = dp[i][j-2] or (
                    dp[i-1][j] and (p[j-2] == '.' or p[j-2] == s[i-1])
                )
            elif p[j-1] == '.' or p[j-1] == s[i-1]:
                dp[i][j] = dp[i-1][j-1]
    
    return dp[m][n]
```

---

## 📊 State Transitions

```
p[j] == '*':
  - Zero match: dp[i][j-2]
  - One+ match: dp[i-1][j] if p[j-1] matches s[i]

p[j] == '.' or p[j] == s[i]:
  - dp[i-1][j-1]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Handle `*` with preceding char** - Two cases: 0 or 1+ matches
2. **`.` matches any** - Treat as matching any char
3. **Empty pattern init** - Handle x* patterns
4. **Classic DP problem** - String matching

---

## 🔗 Related Problems
- Wildcard Matching
- Edit Distance
