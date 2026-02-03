# Alien Dictionary

## 📋 Problem Statement

There is a new alien language that uses the English alphabet. However, the order of the letters is unknown to you.

You are given a list of strings `words` from the alien language's dictionary, where the strings are sorted lexicographically by the rules of this new language.

Return a string of the unique letters sorted in lexicographically increasing order by the alien language's rules. If there is no valid ordering, return `""`.

### Examples

**Example 1:**
```
Input: words = ["wrt","wrf","er","ett","rftt"]
Output: "wertf"
```

---

## 🧠 Thought Process

### Key Insight 💡
**Topological Sort!**
1. Compare adjacent words to find character ordering
2. Build directed graph of orderings
3. Topological sort to get result

---

## 💡 Solution

```python
from collections import defaultdict, deque

def alienOrder(words: list[str]) -> str:
    # Build adjacency list and indegree
    graph = defaultdict(set)
    indegree = {c: 0 for word in words for c in word}
    
    # Compare adjacent words
    for i in range(len(words) - 1):
        w1, w2 = words[i], words[i + 1]
        min_len = min(len(w1), len(w2))
        
        # Invalid case: prefix is longer
        if len(w1) > len(w2) and w1[:min_len] == w2[:min_len]:
            return ""
        
        for j in range(min_len):
            if w1[j] != w2[j]:
                if w2[j] not in graph[w1[j]]:
                    graph[w1[j]].add(w2[j])
                    indegree[w2[j]] += 1
                break
    
    # Topological sort
    queue = deque([c for c in indegree if indegree[c] == 0])
    result = []
    
    while queue:
        c = queue.popleft()
        result.append(c)
        
        for neighbor in graph[c]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)
    
    if len(result) != len(indegree):
        return ""  # Cycle detected
    
    return ''.join(result)
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(C) |
| Space | O(1) |

Where C = total length of all words

---

## 🎯 Key Takeaways

1. **Adjacent words comparison** - Find ordering constraints
2. **Topological sort** - Resolve orderings
3. **Invalid cases** - Cycle or prefix violation
4. **Include all chars** - Even with no constraints

---

## 🔗 Related Problems
- Course Schedule
- Sequence Reconstruction
