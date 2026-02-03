# Rotate Image

## 📋 Problem Statement

You are given an `n x n` 2D matrix representing an image, rotate the image by **90 degrees** (clockwise).

You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly.

### Examples

**Example 1:**
```
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]

1 2 3      7 4 1
4 5 6  →   8 5 2
7 8 9      9 6 3
```

---

## 🧠 Thought Process

### Key Insight 💡
**90° clockwise = Transpose + Reverse each row**

1. **Transpose:** Swap [i][j] with [j][i]
2. **Reverse rows:** Reverse each row

---

## 💡 Solution

```python
def rotate(matrix: list[list[int]]) -> None:
    n = len(matrix)
    
    # Step 1: Transpose
    for i in range(n):
        for j in range(i + 1, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
    # Step 2: Reverse each row
    for row in matrix:
        row.reverse()
```

---

## 🔍 Detailed Walkthrough

```
Original:
1 2 3
4 5 6
7 8 9

After Transpose:
1 4 7
2 5 8
3 6 9

After Reverse Rows:
7 4 1
8 5 2
9 6 3 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n²) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Transpose + Reverse = 90° rotation**
2. **In-place transformation** - No extra space
3. **j starts from i+1** - Avoid swapping twice

---

## 🔗 Related Problems
- Spiral Matrix
- Set Matrix Zeroes
- Rotate Array
