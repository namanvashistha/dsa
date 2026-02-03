# Daily Temperatures

## 📋 Problem Statement

Given an array of integers `temperatures` represents the daily temperatures, return an array `answer` such that `answer[i]` is the number of days you have to wait after the `i`th day to get a warmer temperature. If there is no future day for which this is possible, keep `answer[i] == 0` instead.

### Examples

**Example 1:**
```
Input: temperatures = [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

**Example 2:**
```
Input: temperatures = [30,40,50,60]
Output: [1,1,1,0]
```

### Constraints
- `1 <= temperatures.length <= 10^5`
- `30 <= temperatures[i] <= 100`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- For each day, find next warmer day
- Return distance (in days) to that warmer day
- If no warmer day exists, return 0

### Step 2: Key Insight 💡
Use **Monotonic Decreasing Stack**:
- Stack stores indices of days waiting for warmer day
- When we find a warmer day, pop and record the distance
- Maintain decreasing order (by temperature)

---

## 💡 Solution

```python
def dailyTemperatures(temperatures: list[int]) -> list[int]:
    n = len(temperatures)
    answer = [0] * n
    stack = []  # Store indices
    
    for i in range(n):
        # Pop all days that found their warmer day
        while stack and temperatures[stack[-1]] < temperatures[i]:
            prev_idx = stack.pop()
            answer[prev_idx] = i - prev_idx
        
        stack.append(i)
    
    return answer
```

---

## 🔍 Detailed Walkthrough

### Example: `temperatures = [73, 74, 75, 71, 69, 72, 76, 73]`

```
i=0, temp=73:
  stack empty → push 0
  stack = [0]

i=1, temp=74:
  temp[0]=73 < 74 → pop, answer[0] = 1-0 = 1
  stack = []
  push 1
  stack = [1]

i=2, temp=75:
  temp[1]=74 < 75 → pop, answer[1] = 2-1 = 1
  stack = []
  push 2
  stack = [2]

i=3, temp=71:
  temp[2]=75 > 71 → keep
  push 3
  stack = [2, 3]

i=4, temp=69:
  temp[3]=71 > 69 → keep
  push 4
  stack = [2, 3, 4]

i=5, temp=72:
  temp[4]=69 < 72 → pop, answer[4] = 5-4 = 1
  temp[3]=71 < 72 → pop, answer[3] = 5-3 = 2
  temp[2]=75 > 72 → keep
  push 5
  stack = [2, 5]

i=6, temp=76:
  temp[5]=72 < 76 → pop, answer[5] = 6-5 = 1
  temp[2]=75 < 76 → pop, answer[2] = 6-2 = 4
  stack = []
  push 6
  stack = [6]

i=7, temp=73:
  temp[6]=76 > 73 → keep
  push 7
  stack = [6, 7]

Remaining in stack: no warmer day → answer stays 0

Result: [1, 1, 4, 2, 1, 1, 0, 0] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

**Why O(n)?** Each index is pushed and popped at most once.

---

## 🎯 Key Takeaways

1. **Monotonic stack for "next greater"** - Classic pattern!
2. **Store indices, not values** - Need to calculate distance
3. **Process when found** - Pop and record immediately
4. **Remaining stack = no answer** - Left as 0

---

## 🔗 Related Problems
- Next Greater Element I, II
- Largest Rectangle in Histogram
- Stock Span Problem
- 132 Pattern
