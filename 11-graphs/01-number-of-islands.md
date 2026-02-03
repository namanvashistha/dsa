# Number of Islands

## 📋 Problem Statement

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return the number of islands.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically.

### Examples

**Example 1:**
```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

**Example 2:**
```
Input: grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
Output: 3
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Count connected components of '1's
- Adjacent = up, down, left, right
- Each island = one connected component

### Step 2: Key Insight 💡
For each unvisited '1':
1. Increment island count
2. DFS/BFS to mark all connected '1's as visited

---

## 💡 Solution

```python
def numIslands(grid: list[list[str]]) -> int:
    if not grid:
        return 0
    
    rows, cols = len(grid), len(grid[0])
    islands = 0
    
    def dfs(r, c):
        if (r < 0 or r >= rows or 
            c < 0 or c >= cols or 
            grid[r][c] != '1'):
            return
        
        grid[r][c] = '0'  # Mark as visited
        
        dfs(r + 1, c)
        dfs(r - 1, c)
        dfs(r, c + 1)
        dfs(r, c - 1)
    
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == '1':
                islands += 1
                dfs(r, c)
    
    return islands
```

---

## 🔍 Detailed Walkthrough

```
Grid:
1 1 0
1 0 0
0 0 1

(0,0) = '1': island count = 1, DFS marks (0,0), (0,1), (1,0)
(2,2) = '1': island count = 2, DFS marks (2,2)

Result: 2 islands ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Grid as graph** - Cells are nodes, adjacent cells are edges
2. **DFS/BFS for connected components** - Classic pattern
3. **Mark visited in-place** - Modify '1' to '0'
4. **Count DFS calls** - Each call = one island

---

## 🔗 Related Problems
- Max Area of Island
- Surrounded Regions
- Pacific Atlantic Water Flow
- Number of Provinces
