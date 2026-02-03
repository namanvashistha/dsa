# Palindrome Partitioning

## 📋 Problem Statement

Given a string `s`, partition `s` such that every substring of the partition is a palindrome. Return all possible palindrome partitioning of `s`.

### Examples

**Example 1:**
```
Input: s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

---

## 💡 Solution

```python
def partition(s: str) -> list[list[str]]:
    result = []
    
    def is_palindrome(sub):
        return sub == sub[::-1]
    
    def backtrack(start, path):
        if start == len(s):
            result.append(path.copy())
            return
        
        for end in range(start + 1, len(s) + 1):
            substring = s[start:end]
            if is_palindrome(substring):
                path.append(substring)
                backtrack(end, path)
                path.pop()
    
    backtrack(0, [])
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × 2^n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Try all partitions** - Backtracking
2. **Only continue if palindrome** - Pruning
3. **Base case** - When start reaches end
4. **Can precompute palindromes** - DP optimization

---

## 🔗 Related Problems
- Palindrome Partitioning II (min cuts)
- Longest Palindromic Substring
