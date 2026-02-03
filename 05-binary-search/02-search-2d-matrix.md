# Search a 2D Matrix

## 📋 Problem Statement

You are given an `m x n` integer matrix with the following properties:
- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if target is in the matrix, or `false` otherwise.

You must write a solution in `O(log(m * n))` time complexity.

### Examples

**Example 1:**
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

---

## 🧠 Thought Process

### Key Insight 💡
Treat the 2D matrix as a **1D sorted array**!
- Index i → row = i // cols, col = i % cols
- Single binary search on virtual 1D array

---

## 💡 Solution

```python
def searchMatrix(matrix: list[list[int]], target: int) -> bool:
    rows, cols = len(matrix), len(matrix[0])
    left, right = 0, rows * cols - 1
    
    while left <= right:
        mid = (left + right) // 2
        # Convert 1D index to 2D
        row, col = mid // cols, mid % cols
        value = matrix[row][col]
        
        if value == target:
            return True
        elif value < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return False
```

---

## 🔍 Detailed Walkthrough

```
matrix = [[1,3,5,7],
          [10,11,16,20],
          [23,30,34,60]]
target = 3

Virtual 1D: [1,3,5,7,10,11,16,20,23,30,34,60]
left=0, right=11

mid=5: row=5//4=1, col=5%4=1 → 11 > 3
       right=4

mid=2: row=2//4=0, col=2%4=2 → 5 > 3
       right=1

mid=0: row=0//4=0, col=0%4=0 → 1 < 3
       left=1

mid=1: row=1//4=0, col=1%4=1 → 3 == 3 ✓

Result: True ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(log(m×n)) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **2D → 1D mapping** - row = i // cols, col = i % cols
2. **Single binary search** - Treat as sorted 1D array
3. **Meets O(log(m×n))** - Required complexity

---

## 🔗 Related Problems
- Search a 2D Matrix II (different properties)
- Kth Smallest Element in a Sorted Matrix
