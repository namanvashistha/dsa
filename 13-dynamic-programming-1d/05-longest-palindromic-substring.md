# Longest Palindromic Substring

## 📋 Problem Statement

Given a string `s`, return the longest palindromic substring in `s`.

### Examples

**Example 1:**
```
Input: s = "babad"
Output: "bab" or "aba"
```

**Example 2:**
```
Input: s = "cbbd"
Output: "bb"
```

---

## 🧠 Thought Process

### Key Insight 💡
**Expand around center!**
- Each char could be center (odd length)
- Each pair could be center (even length)
- Expand outward while palindrome

---

## 💡 Solution

```python
def longestPalindrome(s: str) -> str:
    result = ""
    
    def expand(l, r):
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1:r]
    
    for i in range(len(s)):
        # Odd length
        odd = expand(i, i)
        if len(odd) > len(result):
            result = odd
        
        # Even length
        even = expand(i, i + 1)
        if len(even) > len(result):
            result = even
    
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n²) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Expand from center** - Simple and efficient
2. **Two cases** - Odd and even length
3. **Each position = potential center**
4. **O(1) space** - No DP table needed

---

## 🔗 Related Problems
- Palindromic Substrings (count)
- Longest Palindromic Subsequence
