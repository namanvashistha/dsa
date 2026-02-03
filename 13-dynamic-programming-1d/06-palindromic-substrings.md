# Palindromic Substrings

## 📋 Problem Statement

Given a string `s`, return the number of palindromic substrings in it.

### Examples

**Example 1:**
```
Input: s = "abc"
Output: 3
Explanation: "a", "b", "c"
```

**Example 2:**
```
Input: s = "aaa"
Output: 6
Explanation: "a", "a", "a", "aa", "aa", "aaa"
```

---

## 💡 Solution

```python
def countSubstrings(s: str) -> int:
    count = 0
    
    def expand(l, r):
        nonlocal count
        while l >= 0 and r < len(s) and s[l] == s[r]:
            count += 1
            l -= 1
            r += 1
    
    for i in range(len(s)):
        expand(i, i)      # Odd length
        expand(i, i + 1)  # Even length
    
    return count
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n²) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Same expand approach** - As longest palindrome
2. **Count each valid expansion** - Instead of tracking longest
3. **Each single char = palindrome**

---

## 🔗 Related Problems
- Longest Palindromic Substring
