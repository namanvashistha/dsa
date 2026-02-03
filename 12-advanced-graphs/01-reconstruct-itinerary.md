# Reconstruct Itinerary

## 📋 Problem Statement

You are given a list of airline `tickets` where `tickets[i] = [fromi, toi]` represent the departure and arrival airports. Reconstruct the itinerary in order and return it.

All tickets belong to a man who departs from `"JFK"`, thus the itinerary must begin with `"JFK"`. If there are multiple valid itineraries, return the one with the smallest lexical order.

You must use all the tickets exactly once.

### Examples

**Example 1:**
```
Input: tickets = [["MUC","LHR"],["JFK","MUC"],["SFO","SJC"],["LHR","SFO"]]
Output: ["JFK","MUC","LHR","SFO","SJC"]
```

---

## 🧠 Thought Process

### Key Insight 💡
**Eulerian Path** - Visit every edge exactly once.
- Use Hierholzer's algorithm
- Sort destinations for lexical order
- Post-order DFS

---

## 💡 Solution

```python
from collections import defaultdict

def findItinerary(tickets: list[list[str]]) -> list[str]:
    graph = defaultdict(list)
    
    # Sort in reverse for efficient pop
    for src, dst in sorted(tickets, reverse=True):
        graph[src].append(dst)
    
    result = []
    
    def dfs(airport):
        while graph[airport]:
            dfs(graph[airport].pop())
        result.append(airport)
    
    dfs("JFK")
    return result[::-1]
```

---

## 🔍 Walkthrough

```
Tickets: JFK→MUC, MUC→LHR, LHR→SFO, SFO→SJC

Graph (sorted reverse):
JFK: [MUC]
MUC: [LHR]
LHR: [SFO]
SFO: [SJC]

DFS from JFK:
JFK → MUC → LHR → SFO → SJC (stuck)
Add: SJC, SFO, LHR, MUC, JFK

Reverse: JFK → MUC → LHR → SFO → SJC
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(E log E) |
| Space | O(E) |

---

## 🎯 Key Takeaways

1. **Hierholzer's algorithm** - Eulerian path
2. **Post-order append** - Build path backwards
3. **Sort reverse + pop** - Lexical order
4. **Use all edges once** - Eulerian constraint

---

## 🔗 Related Problems
- Alien Dictionary
- Valid Arrangement of Pairs
