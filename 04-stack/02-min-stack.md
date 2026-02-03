# Min Stack

## 📋 Problem Statement

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:
- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.

### Examples

```
Input: ["MinStack","push","push","push","getMin","pop","top","getMin"]
       [[],[-2],[0],[-3],[],[],[],[]]
Output: [null,null,null,null,-3,null,0,-2]
```

---

## 🧠 Thought Process

### Step 1: Challenge
How to track minimum in O(1) when elements are popped?

### Step 2: Key Insight 💡
Store minimum **at each state** of the stack!

Each entry: (value, min_so_far)

---

## 💡 Solution

```python
class MinStack:
    def __init__(self):
        self.stack = []  # Each element: (val, current_min)
    
    def push(self, val: int) -> None:
        if not self.stack:
            self.stack.append((val, val))
        else:
            current_min = min(val, self.stack[-1][1])
            self.stack.append((val, current_min))
    
    def pop(self) -> None:
        self.stack.pop()
    
    def top(self) -> int:
        return self.stack[-1][0]
    
    def getMin(self) -> int:
        return self.stack[-1][1]
```

---

## 📊 Alternative: Two Stacks

```python
class MinStack:
    def __init__(self):
        self.stack = []
        self.min_stack = []
    
    def push(self, val: int) -> None:
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)
    
    def pop(self) -> None:
        if self.stack.pop() == self.min_stack[-1]:
            self.min_stack.pop()
    
    def top(self) -> int:
        return self.stack[-1]
    
    def getMin(self) -> int:
        return self.min_stack[-1]
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| push | O(1) | O(n) |
| pop | O(1) | - |
| top | O(1) | - |
| getMin | O(1) | - |

---

## 🎯 Key Takeaways

1. **Store min with each element** - Track history
2. **Two stacks approach** - Separate min tracking
3. **O(1) operations** - Design requirement met
4. **Classic design pattern** - Auxiliary data structure

---

## 🔗 Related Problems
- Max Stack
- Stack with Increment Operation
- Design a Stack With Increment Operation
