# Spiral Matrix

## 📋 Problem Statement

Given an `m x n` matrix, return all elements of the matrix in spiral order.

### Examples

**Example 1:**
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]

1 → 2 → 3
        ↓
4 → 5   6
↑       ↓
7 ← 8 ← 9
```

---

## 🧠 Thought Process

### Key Insight 💡
Use **four boundaries**: top, bottom, left, right
Spiral: right → down → left → up, shrink boundaries.

---

## 💡 Solution

```python
def spiralOrder(matrix: list[list[int]]) -> list[int]:
    result = []
    top, bottom = 0, len(matrix) - 1
    left, right = 0, len(matrix[0]) - 1
    
    while top <= bottom and left <= right:
        # Right
        for col in range(left, right + 1):
            result.append(matrix[top][col])
        top += 1
        
        # Down
        for row in range(top, bottom + 1):
            result.append(matrix[row][right])
        right -= 1
        
        # Left (check if row exists)
        if top <= bottom:
            for col in range(right, left - 1, -1):
                result.append(matrix[bottom][col])
            bottom -= 1
        
        # Up (check if column exists)
        if left <= right:
            for row in range(bottom, top - 1, -1):
                result.append(matrix[row][left])
            left += 1
    
    return result
```

---

## 📊 Visual Walkthrough

```
1  2  3
4  5  6
7  8  9

top=0, bottom=2, left=0, right=2

Right: 1,2,3 → top=1
Down: 6,9 → right=1
Left: 8,7 → bottom=1
Up: 4 → left=1

Right: 5 → top=2

Result: [1,2,3,6,9,8,7,4,5] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Four boundaries** - Shrink after each direction
2. **Check before left/up** - Handle single row/column
3. **Classic matrix pattern** - Many variations

---

## 🔗 Related Problems
- Spiral Matrix II (generate)
- Rotate Image
- Diagonal Traverse
