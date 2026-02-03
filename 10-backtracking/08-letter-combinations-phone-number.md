# Letter Combinations of a Phone Number

## 📋 Problem Statement

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

### Examples

**Example 1:**
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

---

## 💡 Solution

```python
def letterCombinations(digits: str) -> list[str]:
    if not digits:
        return []
    
    phone = {
        '2': 'abc', '3': 'def', '4': 'ghi', '5': 'jkl',
        '6': 'mno', '7': 'pqrs', '8': 'tuv', '9': 'wxyz'
    }
    
    result = []
    
    def backtrack(i, path):
        if i == len(digits):
            result.append(''.join(path))
            return
        
        for char in phone[digits[i]]:
            path.append(char)
            backtrack(i + 1, path)
            path.pop()
    
    backtrack(0, [])
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(4^n × n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Phone mapping** - Digit to letters
2. **Cartesian product** - Try all combinations
3. **Standard backtracking** - Try, recurse, undo

---

## 🔗 Related Problems
- Generate Parentheses
- Combinations
