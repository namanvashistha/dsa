# 📚 Stack - NeetCode 150

> 7 problems | Master LIFO for matching, monotonic stacks, and evaluation

---

## 1️⃣ Valid Parentheses ⭐ Easy
**The Trick:** Stack for matching pairs
- Opening bracket → push to stack
- Closing bracket → pop and check match
- End: stack should be empty
- **Remember:** Stack = LIFO = perfect for nesting

---

## 2️⃣ Min Stack ⭐⭐ Medium
**The Trick:** Two stacks (main + min tracker)
- Main stack: normal operations
- Min stack: tracks minimum at each level
- Push/pop from both simultaneously
- **Remember:** Parallel min stack synced with main

---

## 3️⃣ Evaluate Reverse Polish Notation ⭐⭐ Medium
**The Trick:** Numbers → push; Operators → pop two and compute
- If number → push to stack
- If operator → pop two, compute, push result
- Left operand is second pop!
- **Remember:** `b = pop(); a = pop(); push(a op b)`

---

## 4️⃣ Generate Parentheses ⭐⭐ Medium
**The Trick:** Backtracking with open/close count
- Add '(' if open < n
- Add ')' if close < open
- Valid when open = close = n
- **Remember:** More opens available, closes follow opens

---

## 5️⃣ Daily Temperatures ⭐⭐ Medium
**The Trick:** Monotonic decreasing stack (indices)
- Store indices in stack
- Current temp > stack top → found warmer day
- Pop and calculate distance
- **Remember:** Stack stores waiting days (indices)

---

## 6️⃣ Car Fleet ⭐⭐ Medium
**The Trick:** Sort by position, stack by arrival time
- Calculate time to reach target for each car
- Sort by position (closest to target first)
- If slower car ahead → forms fleet
- **Remember:** Cars at same time = one fleet

---

## 7️⃣ Largest Rectangle in Histogram ⭐⭐⭐ Hard
**The Trick:** Monotonic increasing stack (indices)
- Stack stores indices of increasing heights
- When smaller height → pop and calculate area
- Area = `height[popped] × (current - stack_top - 1)`
- **Remember:** Stack keeps increasing, pop when decreasing

---

## 🎯 Pattern Recognition

**Use Stack when:**
- Matching pairs (parentheses, brackets)
- Nested structures
- Need to track previous elements
- "Next greater/smaller element" problems
- Evaluate expressions (postfix, prefix)

**Stack Types:**

1. **Regular Stack:** LIFO operations
   - Valid parentheses
   - Expression evaluation
   - Undo/redo operations

2. **Monotonic Stack:** Maintain order
   - **Increasing:** Find next smaller
   - **Decreasing:** Find next greater
   - Store indices, not values

**Monotonic Stack Template:**
```
stack = []
for i in range(len(arr)):
    while stack and arr[stack[-1]] > arr[i]:  # decreasing
        # Found next smaller for stack[-1]
        idx = stack.pop()
        # process idx
    stack.append(i)
```

**Common Mistakes:**
- Forgetting to check if stack is empty before pop
- Storing values instead of indices (for monotonic)
- Wrong order of operands in RPN
- Not handling edge cases (empty input)

**Key Insight:**
- Stack sees elements in **reverse order** when popping
- Perfect for "closest previous/next" problems
