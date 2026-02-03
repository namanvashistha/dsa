# Surrounded Regions

## 📋 Problem Statement

Given an `m x n` matrix `board` containing `'X'` and `'O'`, capture all regions that are 4-directionally surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

### Examples

**Example 1:**
```
Input: board = [["X","X","X","X"],
                ["X","O","O","X"],
                ["X","X","O","X"],
                ["X","O","X","X"]]
Output: [["X","X","X","X"],
         ["X","X","X","X"],
         ["X","X","X","X"],
         ["X","O","X","X"]]
```

---

## 🧠 Thought Process

### Key Insight 💡
**Reverse thinking!**
- O's on border can't be captured
- Mark border-connected O's as safe
- Flip remaining O's to X's

---

## 💡 Solution

```python
def solve(board: list[list[str]]) -> None:
    rows, cols = len(board), len(board[0])
    
    def dfs(r, c):
        if (r < 0 or r >= rows or 
            c < 0 or c >= cols or 
            board[r][c] != 'O'):
            return
        
        board[r][c] = 'S'  # Safe
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)
    
    # Mark border-connected O's
    for r in range(rows):
        dfs(r, 0)
        dfs(r, cols - 1)
    for c in range(cols):
        dfs(0, c)
        dfs(rows - 1, c)
    
    # Flip O's to X's, restore S's to O's
    for r in range(rows):
        for c in range(cols):
            if board[r][c] == 'O':
                board[r][c] = 'X'
            elif board[r][c] == 'S':
                board[r][c] = 'O'
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Border O's = safe** - Can't be surrounded
2. **Mark safe first** - Then flip rest
3. **Temporary marker** - 'S' for safe
4. **In-place modification** - Two passes

---

## 🔗 Related Problems
- Number of Islands
- Number of Enclaves
