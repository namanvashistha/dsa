# Swim in Rising Water

## 📋 Problem Statement

You are given an `n x n` integer matrix `grid` where each value `grid[i][j]` represents the elevation at that point.

Rain starts to fall. At time `t`, the depth of the water everywhere is `t`. You can swim from a cell to any adjacent cell if and only if both cells have elevation at most `t`.

Find the least time until you can reach the bottom right square `(n-1, n-1)` starting from the top left `(0, 0)`.

### Examples

**Example 1:**
```
Input: grid = [[0,2],[1,3]]
Output: 3
```

---

## 🧠 Thought Process

### Key Insight 💡
**Binary Search + BFS** or **Dijkstra's**
- Minimum time = maximum elevation on path
- Find path minimizing the maximum elevation

---

## 💡 Solution: Dijkstra's

```python
import heapq

def swimInWater(grid: list[list[int]]) -> int:
    n = len(grid)
    visited = set()
    heap = [(grid[0][0], 0, 0)]  # (time, row, col)
    
    while heap:
        time, r, c = heapq.heappop(heap)
        
        if r == n - 1 and c == n - 1:
            return time
        
        if (r, c) in visited:
            continue
        
        visited.add((r, c))
        
        for dr, dc in [(0,1), (0,-1), (1,0), (-1,0)]:
            nr, nc = r + dr, c + dc
            
            if (0 <= nr < n and 
                0 <= nc < n and 
                (nr, nc) not in visited):
                heapq.heappush(heap, (max(time, grid[nr][nc]), nr, nc))
    
    return -1
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n² log n) |
| Space | O(n²) |

---

## 🎯 Key Takeaways

1. **Max elevation on path** - Not sum of elevations
2. **Dijkstra's modified** - Priority = max elevation so far
3. **Min-heap** - Explore lowest max-elevation path first
4. **First to reach = answer** - Optimal path

---

## 🔗 Related Problems
- Path With Minimum Effort
- Network Delay Time
