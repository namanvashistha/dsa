# Walls and Gates

## 📋 Problem Statement

You are given an `m x n` grid `rooms` initialized with:
- `-1` A wall or an obstacle
- `0` A gate
- `INF` An empty room (2147483647)

Fill each empty room with the distance to its nearest gate. If it is impossible to reach a gate, leave as `INF`.

### Examples

```
Input: rooms = [[INF,-1,0,INF],
                [INF,INF,INF,-1],
                [INF,-1,INF,-1],
                [0,-1,INF,INF]]
Output: [[3,-1,0,1],
         [2,2,1,-1],
         [1,-1,2,-1],
         [0,-1,3,4]]
```

---

## 🧠 Thought Process

### Key Insight 💡
**Multi-source BFS from gates!**
- Start from all gates simultaneously
- Each level = +1 distance
- Update room distances

---

## 💡 Solution

```python
from collections import deque

def wallsAndGates(rooms: list[list[int]]) -> None:
    if not rooms:
        return
    
    rows, cols = len(rooms), len(rooms[0])
    INF = 2147483647
    queue = deque()
    
    # Add all gates to queue
    for r in range(rows):
        for c in range(cols):
            if rooms[r][c] == 0:
                queue.append((r, c))
    
    directions = [(0,1), (0,-1), (1,0), (-1,0)]
    
    while queue:
        r, c = queue.popleft()
        
        for dr, dc in directions:
            nr, nc = r + dr, c + dc
            
            if (0 <= nr < rows and 
                0 <= nc < cols and 
                rooms[nr][nc] == INF):
                rooms[nr][nc] = rooms[r][c] + 1
                queue.append((nr, nc))
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(m × n) |
| Space | O(m × n) |

---

## 🎯 Key Takeaways

1. **Multi-source BFS** - Start from all gates
2. **Level = distance** - Natural BFS property
3. **Only update INF cells** - Skip walls/gates
4. **In-place update** - Modify input

---

## 🔗 Related Problems
- Rotting Oranges
- Shortest Path in Binary Matrix
