# Partition Labels

## 📋 Problem Statement

You are given a string `s`. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Return a list of integers representing the size of these parts.

### Examples

**Example 1:**
```
Input: s = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation: "ababcbaca", "defegde", "hijhklij"
```

---

## 💡 Solution

```python
def partitionLabels(s: str) -> list[int]:
    # Last occurrence of each character
    last = {c: i for i, c in enumerate(s)}
    
    result = []
    start = 0
    end = 0
    
    for i, c in enumerate(s):
        end = max(end, last[c])
        
        if i == end:
            result.append(end - start + 1)
            start = i + 1
    
    return result
```

---

## 🔍 Walkthrough

```
s = "ababcbacadefegdehijhklij"
last = {a:8, b:5, c:7, d:14, e:15, f:11, g:13, h:19, i:22, j:23, k:20, l:21}

i=0: end=8
i=8: i==end → partition [0,8], size=9

Continue with next partition...
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Last occurrence map** - Find where each char ends
2. **Extend partition** - To include all chars
3. **Close partition** - When current = end
4. **Greedy approach** - Smallest possible partitions

---

## 🔗 Related Problems
- Merge Intervals
- Task Scheduler
