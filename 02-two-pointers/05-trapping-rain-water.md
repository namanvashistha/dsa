# Trapping Rain Water

## 📋 Problem Statement

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

### Examples

**Example 1:**
```
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The elevation map is shown below.
```

```
       ┌──┐
   ┌──┐█  █┌──┐   ┌──┐
   │  █│  ██  █┌──┤  │
───┴──┴┴──┴┴──┴┴──┴──┴───
 0  1  0  2  1  0  1  3  2  1  2  1
```
█ represents trapped water

**Example 2:**
```
Input: height = [4,2,0,3,2,5]
Output: 9
```

### Constraints
- `n == height.length`
- `1 <= n <= 2 * 10^4`
- `0 <= height[i] <= 10^5`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Water collects in valleys between bars
- Water level at any position = min(max_left, max_right) - height[i]
- If max_left or max_right < height[i], no water at that position

### Step 2: Key Insight 💡

For each position i:
```
water[i] = min(max_left[i], max_right[i]) - height[i]
```

Where:
- `max_left[i]` = maximum height to the left of i (inclusive)
- `max_right[i]` = maximum height to the right of i (inclusive)

### Step 3: Approaches
1. **Brute Force:** For each position, scan left and right - O(n²)
2. **DP/Prefix arrays:** Precompute max_left and max_right - O(n) time, O(n) space
3. **Two Pointers:** Compute on the fly - O(n) time, O(1) space

---

## 💡 Solution Approaches

### Approach 1: DP with Prefix/Suffix Arrays

```python
def trap(height: list[int]) -> int:
    if not height:
        return 0
    
    n = len(height)
    
    # max_left[i] = max height from 0 to i
    max_left = [0] * n
    max_left[0] = height[0]
    for i in range(1, n):
        max_left[i] = max(max_left[i - 1], height[i])
    
    # max_right[i] = max height from i to n-1
    max_right = [0] * n
    max_right[n - 1] = height[n - 1]
    for i in range(n - 2, -1, -1):
        max_right[i] = max(max_right[i + 1], height[i])
    
    # Calculate water at each position
    water = 0
    for i in range(n):
        water += min(max_left[i], max_right[i]) - height[i]
    
    return water
```

### Approach 2: Two Pointers (Optimal) ⭐

```python
def trap(height: list[int]) -> int:
    if not height:
        return 0
    
    left = 0
    right = len(height) - 1
    left_max = height[left]
    right_max = height[right]
    water = 0
    
    while left < right:
        if left_max < right_max:
            # Water level determined by left_max
            left += 1
            left_max = max(left_max, height[left])
            water += left_max - height[left]
        else:
            # Water level determined by right_max
            right -= 1
            right_max = max(right_max, height[right])
            water += right_max - height[right]
    
    return water
```

---

## 🔍 Detailed Walkthrough (Two Pointers)

### Example: `height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`

```
Initial:
height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
          L                             R
left_max = 0, right_max = 1, water = 0

Step 1: left_max(0) < right_max(1)
  Move left: L=1
  left_max = max(0, 1) = 1
  water += 1 - 1 = 0

Step 2: left_max(1) == right_max(1)
  Move right: R=10
  right_max = max(1, 2) = 2
  water += 2 - 2 = 0

Step 3: left_max(1) < right_max(2)
  Move left: L=2
  left_max = max(1, 0) = 1
  water += 1 - 0 = 1  ← Water trapped!

Step 4: left_max(1) < right_max(2)
  Move left: L=3
  left_max = max(1, 2) = 2
  water += 2 - 2 = 0

Step 5: left_max(2) == right_max(2)
  Move right: R=9
  right_max = max(2, 1) = 2
  water += 2 - 1 = 1  ← Water trapped!

... continue ...

Final: water = 6 ✓
```

---

## 📊 Visual Explanation

```
height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]

         max_left  height  max_right  water_level  trapped
index 0:    0        0        3          0           0
index 1:    1        1        3          1           0
index 2:    1        0        3          1           1 ←
index 3:    2        2        3          2           0
index 4:    2        1        3          2           1 ←
index 5:    2        0        3          2           2 ←
index 6:    2        1        3          2           1 ←
index 7:    3        3        3          3           0
index 8:    3        2        2          2           0
index 9:    3        1        2          2           1 ←
index 10:   3        2        2          2           0
index 11:   3        1        1          1           0

Total: 1 + 1 + 2 + 1 + 1 = 6 ✓
```

---

## 📊 Why Two Pointers Work

**Key insight:** We only need to know the minimum of (max_left, max_right).

- If `left_max < right_max`:
  - Water at left position is determined by `left_max`
  - We don't need exact `right_max`, just know it's higher
  - Safe to calculate water and move left

- If `right_max ≤ left_max`:
  - Water at right position is determined by `right_max`
  - Safe to calculate water and move right

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| DP Arrays | O(n) | O(n) |
| Two Pointers | O(n) | O(1) |

---

## 🎯 Key Takeaways

1. **Water at position = min(max_left, max_right) - height** - Core formula
2. **Two pointers from ends** - Process position with smaller max
3. **Only need the limiting side** - Don't need exact max on both sides
4. **Similar to Container With Most Water** - But collect water at each position

---

## ⚠️ Common Mistakes

1. Confusing with Container With Most Water (different problem!)
2. Wrong update order for left_max/right_max
3. Not handling empty array
4. Calculating water before updating max (get negative)

---

## 🔄 Stack Solution (Alternative)

```python
def trap(height: list[int]) -> int:
    stack = []  # Store indices
    water = 0
    
    for i, h in enumerate(height):
        while stack and height[stack[-1]] < h:
            mid = stack.pop()
            if not stack:
                break
            
            left = stack[-1]
            width = i - left - 1
            bounded_height = min(height[left], h) - height[mid]
            water += width * bounded_height
        
        stack.append(i)
    
    return water
```

This processes water layer by layer horizontally instead of column by column.

---

## 🔗 Related Problems
- Container With Most Water
- Product of Array Except Self (prefix/suffix pattern)
- Largest Rectangle in Histogram
