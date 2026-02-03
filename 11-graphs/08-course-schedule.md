# Course Schedule

## 📋 Problem Statement

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

Return `true` if you can finish all courses. Otherwise, return `false`.

### Examples

**Example 1:**
```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: Take course 0, then course 1.
```

**Example 2:**
```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: Circular dependency - impossible!
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Prerequisites form a directed graph
- Can finish all courses = no cycle in graph
- This is **cycle detection** in directed graph!

### Step 2: Key Insight 💡
Use DFS with three states:
- **Unvisited (0):** Haven't started processing
- **Visiting (1):** Currently in recursion stack
- **Visited (2):** Completely processed

If we visit a "visiting" node → cycle!

---

## 💡 Solution

```python
def canFinish(numCourses: int, prerequisites: list[list[int]]) -> bool:
    # Build adjacency list
    graph = [[] for _ in range(numCourses)]
    for course, prereq in prerequisites:
        graph[course].append(prereq)
    
    # 0 = unvisited, 1 = visiting, 2 = visited
    state = [0] * numCourses
    
    def hasCycle(course):
        if state[course] == 1:  # Cycle detected!
            return True
        if state[course] == 2:  # Already processed
            return False
        
        state[course] = 1  # Mark as visiting
        
        for prereq in graph[course]:
            if hasCycle(prereq):
                return True
        
        state[course] = 2  # Mark as visited
        return False
    
    for course in range(numCourses):
        if hasCycle(course):
            return False
    
    return True
```

---

## 📊 Alternative: Kahn's Algorithm (BFS)

```python
from collections import deque

def canFinish(numCourses: int, prerequisites: list[list[int]]) -> bool:
    indegree = [0] * numCourses
    graph = [[] for _ in range(numCourses)]
    
    for course, prereq in prerequisites:
        graph[prereq].append(course)
        indegree[course] += 1
    
    queue = deque([i for i in range(numCourses) if indegree[i] == 0])
    count = 0
    
    while queue:
        node = queue.popleft()
        count += 1
        
        for neighbor in graph[node]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
    
    return count == numCourses
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(V + E) |
| Space | O(V + E) |

---

## 🎯 Key Takeaways

1. **Cycle detection in directed graph** - Three states DFS
2. **Visiting = in current path** - Finding it again = cycle
3. **Topological sort** - Alternative approach
4. **Graph problems = think DFS/BFS**

---

## 🔗 Related Problems
- Course Schedule II (return order)
- Alien Dictionary
- Minimum Height Trees
