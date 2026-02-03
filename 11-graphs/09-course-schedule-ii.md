# Course Schedule II

## 📋 Problem Statement

There are a total of `numCourses` courses you have to take. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

Return the ordering of courses you should take to finish all courses. If there are multiple valid answers, return any of them. If it is impossible to finish all courses, return an empty array.

### Examples

**Example 1:**
```
Input: numCourses = 4, prerequisites = [[1,0],[2,0],[3,1],[3,2]]
Output: [0,2,1,3] or [0,1,2,3]
```

---

## 🧠 Thought Process

### Key Insight 💡
**Topological Sort!**
- Kahn's Algorithm (BFS) or DFS
- Return order of processing

---

## 💡 Solution: Kahn's Algorithm

```python
from collections import deque

def findOrder(numCourses: int, prerequisites: list[list[int]]) -> list[int]:
    graph = [[] for _ in range(numCourses)]
    indegree = [0] * numCourses
    
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        indegree[course] += 1
    
    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    order = []
    
    while queue:
        node = queue.popleft()
        order.append(node)
        
        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
    
    return order if len(order) == numCourses else []
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(V + E) |
| Space | O(V + E) |

---

## 🎯 Key Takeaways

1. **Topological sort** - DAG ordering
2. **Kahn's algorithm** - BFS with indegree
3. **Start with indegree 0** - No prerequisites
4. **Check length** - Detect cycle

---

## 🔗 Related Problems
- Course Schedule
- Alien Dictionary
