# Container With Most Water

## 📋 Problem Statement

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i`th line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return the maximum amount of water a container can store.

**Note:** You may not slant the container.

### Examples

**Example 1:**
```
Input: height = [1,8,6,2,5,4,8,3,7]
Output: 49
Explanation: Lines at index 1 (height 8) and index 8 (height 7)
Area = min(8, 7) × (8 - 1) = 7 × 7 = 49
```

**Example 2:**
```
Input: height = [1,1]
Output: 1
```

### Constraints
- `n == height.length`
- `2 <= n <= 10^5`
- `0 <= height[i] <= 10^4`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Two vertical lines form a container
- Water level = minimum of two heights (water spills over shorter)
- Area = min(height[left], height[right]) × (right - left)

### Step 2: Brute Force
```python
# Check all pairs - O(n²)
max_area = 0
for i in range(n):
    for j in range(i+1, n):
        area = min(height[i], height[j]) * (j - i)
        max_area = max(max_area, area)
```

### Step 3: Key Insight 💡
Start with widest container (pointers at both ends).

**Which pointer should we move?**
- Moving gives us smaller width
- To potentially get more area, we need taller height
- **Move the shorter line!** The shorter line limits water level
- Moving taller line can only decrease area (or stay same)

### Step 4: Why Move Shorter Line?
```
If left is shorter:
  - Current area limited by left height
  - Moving left might find taller line → more water possible
  - Moving right (taller) won't help since left still limits
```

---

## 💡 Solution

```python
def maxArea(height: list[int]) -> int:
    left = 0
    right = len(height) - 1
    max_water = 0
    
    while left < right:
        # Calculate area
        width = right - left
        h = min(height[left], height[right])
        area = width * h
        max_water = max(max_water, area)
        
        # Move the shorter line
        if height[left] < height[right]:
            left += 1
        else:
            right -= 1
    
    return max_water
```

---

## 🔍 Detailed Walkthrough

### Example: `height = [1, 8, 6, 2, 5, 4, 8, 3, 7]`

```
Index:    0  1  2  3  4  5  6  7  8
Height:   1  8  6  2  5  4  8  3  7

Step 1: L=0, R=8
        │        ┌──┐
        │  ┌──┐  │  │     ┌──┐
        │  │  │  │  │  ┌──┤  │
        │  │  ├──┤  │  │  │  │
        │  │  │  │  ├──┤  │  │
        │  │  │  │  │  │  │  ├──┐
        │  │  │  ├──┤  │  │  │  │
        ├──┤  │  │  │  │  │  │  │
        0  1  2  3  4  5  6  7  8
        L                       R
        
        width = 8, h = min(1, 7) = 1
        area = 8 × 1 = 8
        height[L]=1 < height[R]=7 → L++

Step 2: L=1, R=8
        width = 7, h = min(8, 7) = 7
        area = 7 × 7 = 49 ⭐ max_water = 49
        height[L]=8 > height[R]=7 → R--

Step 3: L=1, R=7
        width = 6, h = min(8, 3) = 3
        area = 6 × 3 = 18 < 49
        height[L]=8 > height[R]=3 → R--

Step 4: L=1, R=6
        width = 5, h = min(8, 8) = 8
        area = 5 × 8 = 40 < 49
        height[L]=8 == height[R]=8 → R-- (or L++)

... continue until L >= R ...

Result: 49 ✓
```

---

## 📊 Visual Representation

```
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]

      8 |    █              █
      7 |    █              █     █
      6 |    █  █           █     █
      5 |    █  █     █     █     █
      4 |    █  █     █  █  █     █
      3 |    █  █     █  █  █  █  █
      2 |    █  █  █  █  █  █  █  █
      1 | █  █  █  █  █  █  █  █  █
        +---------------------------
          0  1  2  3  4  5  6  7  8

Maximum container: indices 1 and 8
Area = min(8, 7) × 7 = 49
```

---

## 📊 Why Greedy Works (Proof Sketch)

Claim: Moving the shorter line never misses the optimal solution.

Proof:
- Let optimal solution use lines at positions i and j
- At some point, our pointers are at positions where one is at i or j
- If the other pointer is at the optimal line's partner, we calculate that area
- If not, we correctly move toward it (moving shorter line)
- We'll eventually reach the optimal pair

The key insight: When one pointer is at the optimal line, moving the OTHER line (if it's shorter) never helps because:
- Width decreases
- Height is still limited by the shorter line

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Two pointers from both ends** - Start with widest
2. **Move the shorter line** - Can't improve by moving taller
3. **Area = min(heights) × width** - Shorter line limits water
4. **Greedy works** - Never miss optimal by moving shorter

---

## ⚠️ Common Mistakes

1. Moving the taller line instead of shorter
2. Not handling equal heights correctly (move either)
3. Using height[left] + height[right] instead of min
4. Forgetting to update max after each calculation

---

## 🔄 Edge Cases

```python
# Two elements
height = [1, 2]  # Area = min(1,2) × 1 = 1

# All same height
height = [5, 5, 5, 5]  # Area = 5 × 3 = 15 (widest)

# Decreasing
height = [5, 4, 3, 2, 1]  # Check various pairs

# Tallest at ends
height = [10, 1, 1, 1, 10]  # Area = 10 × 4 = 40
```

---

## 🔗 Related Problems
- Trapping Rain Water (similar but sum water above each bar)
- Largest Rectangle in Histogram (different calculation)
- Maximum Area of Island (2D version concept)
