# 🗺️ Advanced Graphs - NeetCode 150

> 6 problems | Master shortest paths, MST, and advanced algorithms

---

## 1️⃣ Reconstruct Itinerary ⭐⭐⭐ Hard
**The Trick:** Eulerian path with DFS (Hierholzer's)
- Build graph (adjacency list), sort destinations
- DFS: visit smallest lexical neighbor first
- Add to result in post-order (reverse at end)
- **Remember:** Post-order gives correct itinerary

**Key:** Use all edges exactly once (Eulerian path)

---

## 2️⃣ Min Cost to Connect All Points ⭐⭐ Medium
**The Trick:** Minimum Spanning Tree (MST)
- Calculate all edge costs (Manhattan distance)
- Use Prim's algorithm with min heap OR
- Kruskal's with Union-Find
- **Remember:** MST connects all nodes with min cost

**Prim's:** Start from one node, greedily add closest
**Kruskal's:** Sort edges, add if doesn't form cycle

---

## 3️⃣ Network Delay Time ⭐⭐ Medium
**The Trick:** Dijkstra's shortest path
- Find shortest time to reach all nodes
- Use min heap with (time, node)
- Track visited to avoid reprocessing
- **Remember:** Dijkstra = BFS with priority queue

---

## 4️⃣ Swim in Rising Water ⭐⭐⭐ Hard
**The Trick:** Modified Dijkstra (minimize maximum)
- Path cost = maximum elevation on path
- Use min heap with (max_elevation, x, y)
- **Remember:** Minimize the maximum (not sum)

---

## 5️⃣ Alien Dictionary ⭐⭐⭐ Hard
**The Trick:** Topological sort from word order
- Compare adjacent words to find char order
- Build directed graph of character dependencies
- Topological sort for final order
- Detect cycle → invalid
- **Remember:** Word order → char dependencies → topo sort

**Example:** `["wrt","wrf"]` → `t` before `f`

---

## 6️⃣ Cheapest Flights Within K Stops ⭐⭐ Medium
**The Trick:** Modified Dijkstra/BFS with stop limit
- Track (cost, node, stops)
- Can revisit if found cheaper with fewer stops
- Stop when reached with ≤ k stops
- **Remember:** Dijkstra with constraint (stops)

**Key difference:** May revisit nodes if path has fewer stops

---

## 🎯 Pattern Recognition

**Algorithm Selection:**

| Problem Type | Algorithm | Time Complexity |
|--------------|-----------|-----------------|
| Shortest path (unweighted) | BFS | O(V + E) |
| Shortest path (weighted, non-negative) | Dijkstra | O(E log V) |
| Shortest path (negative edges) | Bellman-Ford | O(VE) |
| All pairs shortest path | Floyd-Warshall | O(V³) |
| Minimum Spanning Tree | Prim's / Kruskal's | O(E log V) |
| Topological Sort | DFS / Kahn's | O(V + E) |

---

## 🔥 Dijkstra's Algorithm

**Use when:** Shortest path with non-negative weights

**Template:**
```python
import heapq

def dijkstra(graph, start):
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    heap = [(0, start)]  # (distance, node)
    visited = set()
    
    while heap:
        dist, node = heapq.heappop(heap)
        
        if node in visited:
            continue
        visited.add(node)
        
        for neighbor, weight in graph[node]:
            new_dist = dist + weight
            if new_dist < distances[neighbor]:
                distances[neighbor] = new_dist
                heapq.heappush(heap, (new_dist, neighbor))
    
    return distances
```

**Key Points:**
- Min heap: process closest node first
- Greedy: always pick smallest distance
- Mark visited to avoid reprocessing
- Won't work with negative weights!

---

## 🌲 Minimum Spanning Tree (MST)

**Problem:** Connect all nodes with minimum total edge weight

### Prim's Algorithm
```python
def prim(graph, n):
    visited = set([0])
    edges = [(weight, 0, neighbor) for neighbor, weight in graph[0]]
    heapq.heapify(edges)
    total_cost = 0
    
    while len(visited) < n:
        weight, u, v = heapq.heappop(edges)
        if v in visited:
            continue
        
        visited.add(v)
        total_cost += weight
        
        for neighbor, w in graph[v]:
            if neighbor not in visited:
                heapq.heappush(edges, (w, v, neighbor))
    
    return total_cost
```

### Kruskal's Algorithm
```python
def kruskal(edges, n):
    edges.sort()  # Sort by weight
    parent = list(range(n))
    
    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])
        return parent[x]
    
    total_cost = 0
    edges_added = 0
    
    for weight, u, v in edges:
        root_u, root_v = find(u), find(v)
        if root_u != root_v:
            parent[root_u] = root_v
            total_cost += weight
            edges_added += 1
            if edges_added == n - 1:
                break
    
    return total_cost
```

**Prim's:** Start from node, grow tree
**Kruskal's:** Sort edges, add if no cycle

---

## 📍 Key Differences

**BFS vs Dijkstra:**
- BFS: unweighted graphs (all edges = 1)
- Dijkstra: weighted graphs (different edge costs)

**Dijkstra vs Bellman-Ford:**
- Dijkstra: faster, non-negative weights only
- Bellman-Ford: handles negative weights, detects negative cycles

**Prim's vs Kruskal's:**
- Prim's: better for dense graphs
- Kruskal's: better for sparse graphs

---

## 🎓 Advanced Concepts

**Eulerian Path:** Path using each edge exactly once
- Required: 0 or 2 nodes with odd degree
- Algorithm: Hierholzer's (DFS with post-order)

**Topological Sort:** Linear ordering of directed acyclic graph
- DFS: post-order (reverse at end)
- Kahn's: process nodes with indegree 0

**Union-Find Optimizations:**
- **Path compression:** Make tree flat during find
- **Union by rank:** Attach smaller tree to larger

---

## ⚠️ Common Mistakes

- Using Dijkstra with negative weights
- Not checking for negative cycles
- Forgetting visited set in Dijkstra
- Wrong edge direction in topological sort
- Not handling disconnected graphs
- Infinite loop in Dijkstra (reprocessing nodes)

---

## 💡 Key Insights

- **Dijkstra = greedy BFS** with priority queue
- **MST = connect all, minimize cost**
- **Topological sort = dependency ordering**
- Weighted graph → consider Dijkstra
- All pairs → consider Floyd-Warshall
- Negative weights → Bellman-Ford
- MST → Prim's (dense) or Kruskal's (sparse)

**When stuck:** Identify if it's shortest path, MST, or topological ordering problem
