# N-Queens

## 📋 Problem Statement

The **n-queens** puzzle is the problem of placing `n` queens on an `n x n` chessboard such that no two queens attack each other.

Given an integer `n`, return all distinct solutions to the n-queens puzzle.

### Examples

**Example 1:**
```
Input: n = 4
Output: [[".Q..","...Q","Q...","..Q."],
         ["..Q.","Q...","...Q",".Q.."]]
```

---

## 🧠 Thought Process

### Key Insight 💡
Place queens row by row:
- Track attacked columns
- Track attacked diagonals (row-col constant)
- Track attacked anti-diagonals (row+col constant)

---

## 💡 Solution

```python
def solveNQueens(n: int) -> list[list[str]]:
    result = []
    board = [['.'] * n for _ in range(n)]
    
    cols = set()
    diags = set()      # row - col
    anti_diags = set() # row + col
    
    def backtrack(row):
        if row == n:
            result.append([''.join(r) for r in board])
            return
        
        for col in range(n):
            if col in cols or (row - col) in diags or (row + col) in anti_diags:
                continue
            
            # Place queen
            board[row][col] = 'Q'
            cols.add(col)
            diags.add(row - col)
            anti_diags.add(row + col)
            
            backtrack(row + 1)
            
            # Remove queen
            board[row][col] = '.'
            cols.remove(col)
            diags.remove(row - col)
            anti_diags.remove(row + col)
    
    backtrack(0)
    return result
```

---

## 📊 Visual: Diagonal Patterns

```
Diagonal (row - col):
  -3 -2 -1  0
  -2 -1  0  1
  -1  0  1  2
   0  1  2  3

Anti-diagonal (row + col):
   0  1  2  3
   1  2  3  4
   2  3  4  5
   3  4  5  6
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n!) |
| Space | O(n²) |

---

## 🎯 Key Takeaways

1. **Row by row** - Natural constraint (one queen per row)
2. **Diagonal check** - row-col is constant
3. **Anti-diagonal check** - row+col is constant
4. **Classic backtracking** - Try, recurse, undo

---

## 🔗 Related Problems
- N-Queens II (count only)
- Sudoku Solver
- Valid Sudoku
