# Task Scheduler

## 📋 Problem Statement

Given a characters array `tasks` representing tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.

There is a cooling interval `n` that means between two same tasks, there must be at least `n` intervals.

Return the least number of units of times that the CPU will take to finish all the given tasks.

### Examples

**Example 1:**
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B
```

---

## 🧠 Thought Process

### Key Insight 💡
Process most frequent tasks first!
- Max heap for frequencies
- Queue for cooling tasks
- Simulate time step by step

---

## 💡 Solution

```python
import heapq
from collections import Counter, deque

def leastInterval(tasks: list[str], n: int) -> int:
    count = Counter(tasks)
    max_heap = [-c for c in count.values()]
    heapq.heapify(max_heap)
    
    queue = deque()  # (count, available_time)
    time = 0
    
    while max_heap or queue:
        time += 1
        
        if max_heap:
            cnt = heapq.heappop(max_heap) + 1  # Process one
            if cnt < 0:
                queue.append((cnt, time + n))
        
        if queue and queue[0][1] == time:
            heapq.heappush(max_heap, queue.popleft()[0])
    
    return time
```

## 💡 Solution: Math

```python
def leastInterval(tasks: list[str], n: int) -> int:
    count = Counter(tasks)
    max_freq = max(count.values())
    max_count = sum(1 for c in count.values() if c == max_freq)
    
    # Formula: (max_freq - 1) * (n + 1) + max_count
    return max(len(tasks), (max_freq - 1) * (n + 1) + max_count)
```

---

## 📊 Math Explanation

```
Tasks: A A A B B B, n = 2

A _ _ A _ _ A  (max_freq=3, slots=(3-1)*3=6)
A B _ A B _ A B

Answer = max(len(tasks), slots + max_count)
       = max(6, 6 + 2) = 8
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Most frequent first** - Greedy approach
2. **Math formula exists** - Elegant solution
3. **Cooling queue** - Track when tasks available
4. **Idle only when needed** - Fill gaps

---

## 🔗 Related Problems
- Reorganize String
- Rearrange String k Distance Apart
