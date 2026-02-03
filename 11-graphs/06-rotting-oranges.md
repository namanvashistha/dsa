# Rotting Oranges

## 📋 Problem Statement

You are given an `m x n` grid where each cell can have one of three values:
- `0` representing an empty cell
- `1` representing a fresh orange
- `2` representing a rotten orange

Every minute, any fresh orange adjacent (4-directionally) to a rotten orange becomes rotten.

Return the minimum number of minutes until no cell has a fresh orange. If impossible, return `-1`.

### Examples

**Example 1:**
```
Input: grid = [[2,1,1],[1,1,0],[0,1,1]]
Output: 4
```

---

## 🧠 Thought Process

### Key Insight 💡
**Multi-source BFS!**
- Start from all rotten oranges simultaneously
- Each level = 1 minute
- Track fresh oranges count

---

## 💡 Solution

```python
from collections import deque

def orangesRotting(grid: list[list[int]]) -> int:
    rows, cols = len(grid), len(grid[0])
    queue = deque()
    fresh = 0
    
    # Initialize
    for r in range(rows):
        for c in range(cols):
            if grid[r][c] == 2:
                queue.append((r, c))
            elif grid[r][c] == 1:
                fresh += 1
    
    if fresh == 0:
        return 0
    
    minutes = 0
    directions = [(0,1), (0,-1), (1,0), (-1,0)]
    
    while queue:
        minutes += 1
        for _ in range(len(queue)):
            r, c = queue.popleft()
            
            for dr, dc in directions:
                nr, nc = r + dr, c + dc
                
                if (0 <= nr < rows and 
                    0 <= nc < cols and 
                    grid[nr][nc] == 1):
                    grid[nr][nc] = 2
                    fresh -= 1
                    queue.append((nr, nc))
    
    return minutes - 1 if fresh == 0 else -1
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Multi-source BFS** - Start from all rotten
2. **Track fresh count** - Know when done
3. **Level = minute** - BFS levels = time
4. **Return -1 if impossible** - Fresh remaining

---

## 🔗 Related Problems
- Walls and Gates
- Shortest Path in Binary Matrix
