# Generate Parentheses

## 📋 Problem Statement

Given `n` pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

### Examples

**Example 1:**
```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

**Example 2:**
```
Input: n = 1
Output: ["()"]
```

---

## 🧠 Thought Process

### Key Insight 💡
Backtracking with constraints:
- Can add `(` if open < n
- Can add `)` if close < open
- Complete when length = 2n

---

## 💡 Solution

```python
def generateParenthesis(n: int) -> list[str]:
    result = []
    
    def backtrack(current, open_count, close_count):
        if len(current) == 2 * n:
            result.append(current)
            return
        
        if open_count < n:
            backtrack(current + '(', open_count + 1, close_count)
        
        if close_count < open_count:
            backtrack(current + ')', open_count, close_count + 1)
    
    backtrack('', 0, 0)
    return result
```

---

## 🔍 Decision Tree

```
n = 2

                ""
                |
               "("
              /   \
           "(("    "()"
            |        |
          "(()"    "()()"  ✓
            |
         "(())"  ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(4^n / √n) |
| Space | O(n) |

This is the nth Catalan number.

---

## 🎯 Key Takeaways

1. **Two choices** - Add ( or )
2. **Constraints** - open < n, close < open
3. **Valid = equal pairs** - Always well-formed
4. **Catalan number** - Count of valid combinations

---

## 🔗 Related Problems
- Valid Parentheses
- Longest Valid Parentheses
- Remove Invalid Parentheses
