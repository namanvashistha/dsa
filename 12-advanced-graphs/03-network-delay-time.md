# Dijkstra's Algorithm - Network Delay Time

## 📋 Problem Statement

You are given a network of `n` nodes, labeled from `1` to `n`. You are also given `times`, a list of travel times as directed edges `times[i] = (ui, vi, wi)`, where `ui` is the source, `vi` is the target, and `wi` is the time to travel from source to target.

Find the time it takes for all nodes to receive the signal if we send a signal from node `k`. Return `-1` if not all nodes can receive it.

### Examples

**Example 1:**
```
Input: times = [[2,1,1],[2,3,1],[3,4,1]], n = 4, k = 2
Output: 2
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find shortest path from k to ALL nodes
- Return maximum of all shortest paths
- This is **single-source shortest path** → Dijkstra!

### Step 2: Dijkstra's Algorithm
- Use min-heap priority queue
- Process nodes in order of distance
- Relax edges (update shorter paths)

---

## 💡 Solution

```python
import heapq
from collections import defaultdict

def networkDelayTime(times: list[list[int]], n: int, k: int) -> int:
    # Build graph
    graph = defaultdict(list)
    for u, v, w in times:
        graph[u].append((v, w))
    
    # Dijkstra's algorithm
    dist = {k: 0}
    heap = [(0, k)]  # (distance, node)
    
    while heap:
        d, node = heapq.heappop(heap)
        
        if d > dist.get(node, float('inf')):
            continue
        
        for neighbor, weight in graph[node]:
            new_dist = d + weight
            if new_dist < dist.get(neighbor, float('inf')):
                dist[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))
    
    if len(dist) != n:
        return -1
    
    return max(dist.values())
```

---

## 📊 Dijkstra's Template

```python
def dijkstra(graph, start, n):
    dist = {start: 0}
    heap = [(0, start)]
    
    while heap:
        d, node = heapq.heappop(heap)
        
        if d > dist.get(node, float('inf')):
            continue  # Already found shorter
        
        for neighbor, weight in graph[node]:
            new_dist = d + weight
            if new_dist < dist.get(neighbor, float('inf')):
                dist[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))
    
    return dist
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O((V + E) log V) |
| Space | O(V + E) |

---

## 🎯 Key Takeaways

1. **Dijkstra = BFS + Priority Queue** - Process closest first
2. **Works for non-negative weights** - Only!
3. **Greedy approach** - Once visited, distance is final
4. **Min heap** - Always pop smallest distance

---

## 🔗 Related Problems
- Cheapest Flights Within K Stops
- Path with Maximum Probability
- Swim in Rising Water
