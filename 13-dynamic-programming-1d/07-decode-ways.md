# Decode Ways

## 📋 Problem Statement

A message containing letters from `A-Z` can be encoded using `'1' -> 'A'`, `'2' -> 'B'`, ..., `'26' -> 'Z'`.

Given a string `s` containing only digits, return the number of ways to decode it.

### Examples

**Example 1:**
```
Input: s = "12"
Output: 2
Explanation: "12" can be decoded as "AB" (1 2) or "L" (12).
```

**Example 2:**
```
Input: s = "226"
Output: 3
Explanation: "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```

---

## 💡 Solution

```python
def numDecodings(s: str) -> int:
    if not s or s[0] == '0':
        return 0
    
    prev2, prev1 = 1, 1
    
    for i in range(1, len(s)):
        curr = 0
        
        # Single digit decode
        if s[i] != '0':
            curr += prev1
        
        # Two digit decode
        two_digit = int(s[i-1:i+1])
        if 10 <= two_digit <= 26:
            curr += prev2
        
        prev2, prev1 = prev1, curr
    
    return prev1
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Two choices** - Take 1 or 2 digits
2. **Valid ranges** - 1-9 for single, 10-26 for double
3. **Handle '0'** - Can't be decoded alone
4. **Similar to Fibonacci** - Sum of previous two

---

## 🔗 Related Problems
- Climbing Stairs
- Decode Ways II
