# Valid Parentheses

## 📋 Problem Statement

Given a string `s` containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

### Examples

**Example 1:**
```
Input: s = "()"
Output: true
```

**Example 2:**
```
Input: s = "()[]{}"
Output: true
```

**Example 3:**
```
Input: s = "(]"
Output: false
```

### Constraints
- `1 <= s.length <= 10^4`
- `s` consists of parentheses only `'()[]{}'`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Opening brackets must have matching closing brackets
- Order matters: `([])` valid, `([)]` invalid
- All brackets must be matched

### Step 2: Key Insight 💡
Use a **Stack**:
- Opening bracket → push to stack
- Closing bracket → pop and check if matches
- End: stack should be empty

**Why Stack?** LIFO matches the nesting nature of brackets!

---

## 💡 Solution

```python
def isValid(s: str) -> bool:
    stack = []
    mapping = {')': '(', '}': '{', ']': '['}
    
    for char in s:
        if char in mapping:  # Closing bracket
            # Pop from stack, or use dummy if empty
            top = stack.pop() if stack else '#'
            
            # Check if matches
            if mapping[char] != top:
                return False
        else:  # Opening bracket
            stack.append(char)
    
    # Stack should be empty at the end
    return len(stack) == 0
```

---

## 🔍 Detailed Walkthrough

### Example: `s = "([{}])"`

```
char='(':
  Opening bracket → push
  stack = ['(']

char='[':
  Opening bracket → push
  stack = ['(', '[']

char='{':
  Opening bracket → push
  stack = ['(', '[', '{']

char='}':
  Closing bracket
  pop → '{', matches mapping['}'] ✓
  stack = ['(', '[']

char=']':
  Closing bracket
  pop → '[', matches mapping[']'] ✓
  stack = ['(']

char=')':
  Closing bracket
  pop → '(', matches mapping[')'] ✓
  stack = []

End: stack is empty → True ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Stack for matching pairs** - Classic pattern!
2. **LIFO = perfect for nesting** - Last opened, first closed
3. **HashMap for bracket pairs** - Clean lookup
4. **Check empty stack at end** - All brackets matched

---

## 🔗 Related Problems
- Longest Valid Parentheses
- Generate Parentheses
- Remove Invalid Parentheses
- Minimum Remove to Make Valid Parentheses
