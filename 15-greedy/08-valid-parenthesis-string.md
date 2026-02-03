# Valid Parenthesis String

## 📋 Problem Statement

Given a string `s` containing only three types of characters: `'('`, `')'` and `'*'`, return `true` if `s` is valid.

`'*'` could be treated as:
- A single right parenthesis `')'`
- A single left parenthesis `'('`
- An empty string `""`

### Examples

**Example 1:**
```
Input: s = "(*))"
Output: true
```

---

## 🧠 Thought Process

### Key Insight 💡
Track the possible range of open parentheses:
- `lo`: minimum possible open count
- `hi`: maximum possible open count

---

## 💡 Solution

```python
def checkValidString(s: str) -> bool:
    lo = 0  # Minimum open parens (treat * as ) or empty)
    hi = 0  # Maximum open parens (treat * as ()
    
    for c in s:
        if c == '(':
            lo += 1
            hi += 1
        elif c == ')':
            lo -= 1
            hi -= 1
        else:  # '*'
            lo -= 1  # Treat as )
            hi += 1  # Treat as (
        
        if hi < 0:
            return False
        
        lo = max(0, lo)  # Can't have negative open
    
    return lo == 0
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Range tracking** - lo to hi possible open parens
2. **Star flexibility** - Try all three options
3. **lo can't be negative** - Floor at 0
4. **hi negative = invalid** - Too many close parens

---

## 🔗 Related Problems
- Valid Parentheses
- Longest Valid Parentheses
