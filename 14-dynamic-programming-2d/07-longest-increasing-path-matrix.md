# Longest Increasing Path in a Matrix

## 📋 Problem Statement

Given an `m x n` integers matrix, return the length of the longest increasing path.

From each cell, you can move in four directions: left, right, up, or down. You may not move diagonally or outside the boundary.

### Examples

**Example 1:**
```
Input: matrix = [[9,9,4],[6,6,8],[2,1,1]]
Output: 4
Explanation: [1, 2, 6, 9]
```

---

## 💡 Solution: DFS + Memoization

```python
def longestIncreasingPath(matrix: list[list[int]]) -> int:
    m, n = len(matrix), len(matrix[0])
    memo = {}
    
    def dfs(r, c):
        if (r, c) in memo:
            return memo[(r, c)]
        
        length = 1
        for dr, dc in [(0,1), (0,-1), (1,0), (-1,0)]:
            nr, nc = r + dr, c + dc
            if (0 <= nr < m and 0 <= nc < n and 
                matrix[nr][nc] > matrix[r][c]):
                length = max(length, 1 + dfs(nr, nc))
        
        memo[(r, c)] = length
        return length
    
    result = 0
    for r in range(m):
        for c in range(n):
            result = max(result, dfs(r, c))
    
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **DFS + memoization** - Avoid recomputation
2. **Strictly increasing** - No cycles
3. **Each cell visited once** - Memo prevents revisit
4. **Start from each cell** - Track global max

---

## 🔗 Related Problems
- Longest Increasing Subsequence
- Number of Increasing Paths
