# Edit Distance

## 📋 Problem Statement

Given two strings `word1` and `word2`, return the minimum number of operations required to convert `word1` to `word2`.

You have the following three operations:
- Insert a character
- Delete a character
- Replace a character

### Examples

**Example 1:**
```
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse → rorse (replace 'h' with 'r')
rorse → rose (remove 'r')
rose → ros (remove 'e')
```

---

## 🧠 Thought Process

### DP Recurrence
For characters at i, j:
- **If match:** dp[i][j] = dp[i-1][j-1]
- **If no match:** min of:
  - Replace: dp[i-1][j-1] + 1
  - Delete: dp[i-1][j] + 1
  - Insert: dp[i][j-1] + 1

---

## 💡 Solution

```python
def minDistance(word1: str, word2: str) -> int:
    m, n = len(word1), len(word2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    # Base cases
    for i in range(m + 1):
        dp[i][0] = i  # Delete all
    for j in range(n + 1):
        dp[0][j] = j  # Insert all
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                dp[i][j] = 1 + min(
                    dp[i-1][j-1],  # Replace
                    dp[i-1][j],    # Delete
                    dp[i][j-1]     # Insert
                )
    
    return dp[m][n]
```

---

## 📊 Visual DP Table

```
      ""  r  o  s
  ""   0  1  2  3
  h    1  1  2  3
  o    2  2  1  2
  r    3  2  2  2
  s    4  3  3  2
  e    5  4  4  3
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Three operations** - Replace, delete, insert
2. **Match = diagonal** - No operation needed
3. **Classic string DP** - Build on subproblems
4. **Base case** - Empty string transformations

---

## 🔗 Related Problems
- One Edit Distance
- Delete Operation for Two Strings
- Minimum ASCII Delete Sum
