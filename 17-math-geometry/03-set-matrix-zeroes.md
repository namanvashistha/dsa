# Set Matrix Zeroes

## 📋 Problem Statement

Given an `m x n` integer matrix, if an element is `0`, set its entire row and column to `0`s.

You must do it **in place**.

### Examples

**Example 1:**
```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

---

## 🧠 Thought Process

### Key Insight 💡
Use first row and first column as markers!
1. Check if first row/col have zeros
2. Use first row/col to mark zeros
3. Set zeros based on markers
4. Handle first row/col separately

---

## 💡 Solution

```python
def setZeroes(matrix: list[list[int]]) -> None:
    m, n = len(matrix), len(matrix[0])
    first_row_zero = any(matrix[0][j] == 0 for j in range(n))
    first_col_zero = any(matrix[i][0] == 0 for i in range(m))
    
    # Mark zeros in first row/col
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][j] == 0:
                matrix[i][0] = 0
                matrix[0][j] = 0
    
    # Set zeros based on markers
    for i in range(1, m):
        for j in range(1, n):
            if matrix[i][0] == 0 or matrix[0][j] == 0:
                matrix[i][j] = 0
    
    # Handle first row
    if first_row_zero:
        for j in range(n):
            matrix[0][j] = 0
    
    # Handle first column
    if first_col_zero:
        for i in range(m):
            matrix[i][0] = 0
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Use matrix as markers** - O(1) space
2. **Handle first row/col separately** - They're used as markers
3. **Order matters** - Mark before zeroing
4. **In-place modification**

---

## 🔗 Related Problems
- Game of Life
- Spiral Matrix
