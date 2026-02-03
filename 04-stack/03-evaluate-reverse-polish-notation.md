# Evaluate Reverse Polish Notation

## 📋 Problem Statement

You are given an array of strings `tokens` that represents an arithmetic expression in Reverse Polish Notation.

Evaluate the expression. Return an integer that represents the value of the expression.

**Note:**
- Valid operators are `+`, `-`, `*`, and `/`.
- Division truncates toward zero.

### Examples

**Example 1:**
```
Input: tokens = ["2","1","+","3","*"]
Output: 9
Explanation: ((2 + 1) * 3) = 9
```

**Example 2:**
```
Input: tokens = ["4","13","5","/","+"]
Output: 6
Explanation: (4 + (13 / 5)) = 6
```

---

## 🧠 Thought Process

### Key Insight 💡
Use a **stack**:
- Number → push to stack
- Operator → pop two operands, compute, push result

---

## 💡 Solution

```python
def evalRPN(tokens: list[str]) -> int:
    stack = []
    operators = {'+', '-', '*', '/'}
    
    for token in tokens:
        if token in operators:
            b = stack.pop()  # Second operand
            a = stack.pop()  # First operand
            
            if token == '+':
                stack.append(a + b)
            elif token == '-':
                stack.append(a - b)
            elif token == '*':
                stack.append(a * b)
            else:  # Division truncates toward zero
                stack.append(int(a / b))
        else:
            stack.append(int(token))
    
    return stack[0]
```

---

## 🔍 Detailed Walkthrough

```
tokens = ["2", "1", "+", "3", "*"]

"2": push 2, stack=[2]
"1": push 1, stack=[2,1]
"+": pop 1,2 → 2+1=3, stack=[3]
"3": push 3, stack=[3,3]
"*": pop 3,3 → 3*3=9, stack=[9]

Result: 9 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Stack for expression evaluation** - Classic use case
2. **Pop order matters** - Second operand first (for - and /)
3. **int(a/b)** - Truncate toward zero in Python

---

## 🔗 Related Problems
- Basic Calculator
- Basic Calculator II
- Parse Lisp Expression
