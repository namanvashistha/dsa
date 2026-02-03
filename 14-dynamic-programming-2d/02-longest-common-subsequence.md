# Longest Common Subsequence

## 📋 Problem Statement

Given two strings `text1` and `text2`, return the length of their longest common subsequence. If there is no common subsequence, return `0`.

A **subsequence** is a sequence that can be derived from another sequence by deleting some or no elements without changing the order of the remaining elements.

### Examples

**Example 1:**
```
Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: LCS is "ace"
```

**Example 2:**
```
Input: text1 = "abc", text2 = "def"
Output: 0
```

---

## 🧠 Thought Process

### Step 1: DP Recurrence
For characters at positions i, j:
- **If match:** 1 + LCS of remaining
- **If no match:** Max of skipping either character

```
if text1[i] == text2[j]:
    dp[i][j] = 1 + dp[i-1][j-1]
else:
    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

---

## 💡 Solution

```python
def longestCommonSubsequence(text1: str, text2: str) -> int:
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]
    
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = 1 + dp[i-1][j-1]
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])
    
    return dp[m][n]
```

---

## 📊 Visual DP Table

```
      ""  a  c  e
  ""   0  0  0  0
  a    0  1  1  1
  b    0  1  1  1
  c    0  1  2  2
  d    0  1  2  2
  e    0  1  2  3
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Match = diagonal + 1** - Include character
2. **No match = max(left, up)** - Skip one character
3. **Classic 2D DP** - Foundation pattern
4. **Space optimization** - Can reduce to O(n)

---

## 🔗 Related Problems
- Longest Palindromic Subsequence
- Edit Distance
- Shortest Common Supersequence
