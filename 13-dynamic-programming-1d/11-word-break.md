# Word Break

## 📋 Problem Statement

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

### Examples

**Example 1:**
```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: "leetcode" = "leet" + "code"
```

**Example 2:**
```
Input: s = "catsandog", wordDict = ["cats","dog","sand","and","cat"]
Output: false
```

---

## 🧠 Thought Process

### DP Recurrence
```
dp[i] = True if s[0:i] can be segmented
dp[i] = any(dp[j] and s[j:i] in wordDict) for j < i
```

---

## 💡 Solution

```python
def wordBreak(s: str, wordDict: list[str]) -> bool:
    word_set = set(wordDict)
    n = len(s)
    dp = [False] * (n + 1)
    dp[0] = True  # Empty string
    
    for i in range(1, n + 1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break
    
    return dp[n]
```

---

## 🔍 Detailed Walkthrough

```
s = "leetcode", wordDict = ["leet", "code"]

dp = [T, F, F, F, F, F, F, F, F]

i=4: s[0:4]="leet" in dict, dp[0]=T → dp[4]=T
     dp = [T, F, F, F, T, F, F, F, F]

i=8: s[4:8]="code" in dict, dp[4]=T → dp[8]=T
     dp = [T, F, F, F, T, F, F, F, T]

Result: True ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n² × m) |
| Space | O(n) |

Where m = max word length (for substring comparison)

---

## 🎯 Key Takeaways

1. **DP on positions** - Can reach position i?
2. **Check all splits** - From each valid position
3. **Use set for O(1) lookup** - Important optimization
4. **Break early** - Once dp[i] is True

---

## 🔗 Related Problems
- Word Break II (return all sentences)
- Concatenated Words
