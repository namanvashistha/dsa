# Pacific Atlantic Water Flow

## 📋 Problem Statement

Given an `m x n` matrix of non-negative integers representing heights, return a list of grid coordinates where water can flow to both the Pacific ocean (top and left edges) and Atlantic ocean (bottom and right edges).

Water can only flow from a cell to another one with height equal or lower.

### Examples

**Example 1:**
```
Input: heights = [[1,2,2,3,5],[3,2,3,4,4],[2,4,5,3,1],[6,7,1,4,5],[5,1,1,2,4]]
Output: [[0,4],[1,3],[1,4],[2,2],[3,0],[3,1],[4,0]]
```

---

## 🧠 Thought Process

### Key Insight 💡
**Reverse thinking!** Instead of checking each cell:
- Start from oceans and go uphill
- Find cells reachable from Pacific
- Find cells reachable from Atlantic
- Return intersection

---

## 💡 Solution

```python
def pacificAtlantic(heights: list[list[int]]) -> list[list[int]]:
    rows, cols = len(heights), len(heights[0])
    pacific = set()
    atlantic = set()
    
    def dfs(r, c, visited, prev_height):
        if (r < 0 or r >= rows or 
            c < 0 or c >= cols or 
            (r, c) in visited or 
            heights[r][c] < prev_height):
            return
        
        visited.add((r, c))
        for dr, dc in [(0,1), (0,-1), (1,0), (-1,0)]:
            dfs(r + dr, c + dc, visited, heights[r][c])
    
    # Start from Pacific (top and left)
    for c in range(cols):
        dfs(0, c, pacific, 0)
    for r in range(rows):
        dfs(r, 0, pacific, 0)
    
    # Start from Atlantic (bottom and right)
    for c in range(cols):
        dfs(rows - 1, c, atlantic, 0)
    for r in range(rows):
        dfs(r, cols - 1, atlantic, 0)
    
    return list(pacific & atlantic)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Reverse flow** - Start from ocean, go uphill
2. **Two BFS/DFS** - One per ocean
3. **Intersection** - Cells in both sets
4. **Edge cells as starting points**

---

## 🔗 Related Problems
- Surrounded Regions
- Number of Islands
