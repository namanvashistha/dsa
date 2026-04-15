# Largest Rectangle in Histogram

## 📋 Problem Statement

Given an array of integers `heights` representing the histogram's bar heights where the width of each bar is `1`, return the area of the largest rectangle in the histogram.

### Examples

**Example 1:**
```
Input: heights = [2,1,5,6,2,3]
Output: 10
Explanation: Rectangle spans bars with heights 5,6 (width=2, height=5)
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
For each bar, find max width rectangle with that bar's height as minimum.

### Step 2: Key Insight 💡
**Monotonic Increasing Stack**:
- For each bar, find first smaller bar on left and right
- Width = right - left - 1

---

## 💡 Solution

```python
def largestRectangleArea(self, heights: List[int]) -> int:
    stack = []  # (index, height)
    max_area = 0

    for i, h in enumerate(heights):
        start = i

        # pop until stack is increasing
        while stack and stack[-1][1] > h:
            index, height = stack.pop()
            max_area = max(max_area, height * (i - index))
            start = index  # extend to left

        stack.append((start, h))

    # process remaining stack
    n = len(heights)
    for index, height in stack:
        max_area = max(max_area, height * (n - index))

    return max_area
```

---

## 🔍 Detailed Walkthrough

```
heights = [2, 1, 5, 6, 2, 3, 0]  (0 is sentinel)

i=0, h=2: push 0, stack=[0]
i=1, h=1: 
  heights[0]=2 > 1 → pop, height=2, width=1, area=2
  push 1, stack=[1]
i=2, h=5: push 2, stack=[1,2]
i=3, h=6: push 3, stack=[1,2,3]
i=4, h=2:
  heights[3]=6 > 2 → pop, height=6, width=1, area=6
  heights[2]=5 > 2 → pop, height=5, width=2, area=10 ⭐
  push 4, stack=[1,4]
i=5, h=3: push 5, stack=[1,4,5]
i=6, h=0:
  pop remaining bars...

Max Area: 10 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Monotonic stack** - Find previous/next smaller
2. **Sentinel value** - Forces all bars to be processed
3. **Width calculation** - Left boundary from stack top
4. **Each element pushed/popped once** - O(n)

---

## 🔗 Related Problems
- Maximal Rectangle (2D version)
- Trapping Rain Water
- Container With Most Water
