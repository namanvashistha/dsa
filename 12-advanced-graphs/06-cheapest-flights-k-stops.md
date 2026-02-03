# Cheapest Flights Within K Stops

## 📋 Problem Statement

There are `n` cities connected by some number of flights. You are given an array `flights` where `flights[i] = [fromi, toi, pricei]`.

Given `src`, `dst`, and `k`, return the cheapest price from `src` to `dst` with at most `k` stops. If there is no such route, return `-1`.

### Examples

**Example 1:**
```
Input: n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], 
       src = 0, dst = 3, k = 1
Output: 700
Explanation: 0 → 1 → 3 (100 + 600 = 700)
```

---

## 🧠 Thought Process

### Key Insight 💡
**Bellman-Ford** with k+1 iterations!
- Need at most k stops = k+1 edges
- Standard Dijkstra's doesn't work (need to consider hops)

---

## 💡 Solution: Bellman-Ford

```python
def findCheapestPrice(n: int, flights: list[list[int]], src: int, dst: int, k: int) -> int:
    INF = float('inf')
    prices = [INF] * n
    prices[src] = 0
    
    for _ in range(k + 1):
        temp = prices.copy()
        
        for u, v, price in flights:
            if prices[u] != INF:
                temp[v] = min(temp[v], prices[u] + price)
        
        prices = temp
    
    return prices[dst] if prices[dst] != INF else -1
```

## 💡 Solution: BFS

```python
from collections import deque

def findCheapestPrice(n: int, flights: list[list[int]], src: int, dst: int, k: int) -> int:
    graph = [[] for _ in range(n)]
    for u, v, price in flights:
        graph[u].append((v, price))
    
    dist = [float('inf')] * n
    dist[src] = 0
    
    queue = deque([(src, 0, 0)])  # (node, cost, stops)
    
    while queue:
        node, cost, stops = queue.popleft()
        
        if stops > k:
            continue
        
        for neighbor, price in graph[node]:
            new_cost = cost + price
            if new_cost < dist[neighbor]:
                dist[neighbor] = new_cost
                queue.append((neighbor, new_cost, stops + 1))
    
    return dist[dst] if dist[dst] != float('inf') else -1
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Bellman-Ford | O(k × E) | O(n) |
| BFS | O(n × k) | O(n) |

---

## 🎯 Key Takeaways

1. **Bellman-Ford** - Limited iterations for k stops
2. **Copy array** - Prevent using updated values in same round
3. **BFS alternative** - Track stops explicitly
4. **Not standard Dijkstra's** - Need hop constraint

---

## 🔗 Related Problems
- Network Delay Time
- Path With Maximum Probability
