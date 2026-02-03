# Min Cost to Connect All Points

## 📋 Problem Statement

You are given an array `points` where `points[i] = [xi, yi]` represents a point on the 2D plane. The cost of connecting two points is the Manhattan distance between them.

Return the minimum cost to make all points connected.

### Examples

**Example 1:**
```
Input: points = [[0,0],[2,2],[3,10],[5,2],[7,0]]
Output: 20
```

---

## 🧠 Thought Process

### Key Insight 💡
**Minimum Spanning Tree!**
- Connect all points with minimum total cost
- Use Prim's or Kruskal's algorithm

---

## 💡 Solution: Prim's Algorithm

```python
import heapq

def minCostConnectPoints(points: list[list[int]]) -> int:
    n = len(points)
    
    def manhattan(i, j):
        return abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1])
    
    visited = set()
    heap = [(0, 0)]  # (cost, point_index)
    total_cost = 0
    
    while len(visited) < n:
        cost, curr = heapq.heappop(heap)
        
        if curr in visited:
            continue
        
        visited.add(curr)
        total_cost += cost
        
        for next_point in range(n):
            if next_point not in visited:
                heapq.heappush(heap, (manhattan(curr, next_point), next_point))
    
    return total_cost
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n² log n) |
| Space | O(n²) |

---

## 🎯 Key Takeaways

1. **MST problem** - Prim's or Kruskal's
2. **Manhattan distance** - Edge weights
3. **Complete graph** - All pairs connected
4. **Greedy selection** - Min heap for next edge

---

## 🔗 Related Problems
- Connecting Cities With Minimum Cost
- Minimum Spanning Tree
