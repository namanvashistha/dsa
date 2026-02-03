# Word Search

## 📋 Problem Statement

Given an `m x n` grid of characters `board` and a string `word`, return `true` if `word` exists in the grid.

The word can be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once.

### Examples

**Example 1:**
```
Input: board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

---

## 💡 Solution

```python
def exist(board: list[list[str]], word: str) -> bool:
    rows, cols = len(board), len(board[0])
    
    def dfs(r, c, i):
        if i == len(word):
            return True
        
        if (r < 0 or r >= rows or 
            c < 0 or c >= cols or 
            board[r][c] != word[i]):
            return False
        
        # Mark visited
        temp = board[r][c]
        board[r][c] = '#'
        
        # Explore neighbors
        found = (dfs(r + 1, c, i + 1) or
                 dfs(r - 1, c, i + 1) or
                 dfs(r, c + 1, i + 1) or
                 dfs(r, c - 1, i + 1))
        
        # Restore
        board[r][c] = temp
        
        return found
    
    for r in range(rows):
        for c in range(cols):
            if dfs(r, c, 0):
                return True
    
    return False
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n × 4^L) |
| Space | O(L) |

Where L = word length

---

## 🎯 Key Takeaways

1. **DFS with backtracking** - Classic pattern
2. **Mark visited in-place** - Use special char
3. **Restore after exploration** - Backtrack
4. **Try all starting cells** - Word can start anywhere

---

## 🔗 Related Problems
- Word Search II (multiple words)
