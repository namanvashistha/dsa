# Jump Game II

## 📋 Problem Statement

You are given a 0-indexed array of integers `nums`. You are initially at the first index of the array.

Each element `nums[i]` represents the maximum length of a forward jump from index `i`.

Return the minimum number of jumps to reach the last index. You can assume you can always reach the last index.

### Examples

**Example 1:**
```
Input: nums = [2,3,1,1,4]
Output: 2
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

---

## 💡 Solution: Greedy

```python
def jump(nums: list[int]) -> int:
    n = len(nums)
    jumps = 0
    current_end = 0
    farthest = 0
    
    for i in range(n - 1):
        farthest = max(farthest, i + nums[i])
        
        if i == current_end:
            jumps += 1
            current_end = farthest
    
    return jumps
```

---

## 🔍 Walkthrough

```
nums = [2, 3, 1, 1, 4]

i=0: farthest = 2, i==current_end → jumps=1, current_end=2
i=1: farthest = 4
i=2: farthest = 4, i==current_end → jumps=2, current_end=4

Result: 2
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Greedy BFS approach** - Level = one jump
2. **Track farthest reachable** - Within current jump range
3. **Jump when reaching end** - Of current level
4. **Stop before last** - Don't count unnecessary jump

---

## 🔗 Related Problems
- Jump Game
- Jump Game III
