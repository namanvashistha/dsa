# Jump Game

## 📋 Problem Statement

You are given an integer array `nums`. You are initially positioned at the array's first index, and each element represents your maximum jump length at that position.

Return `true` if you can reach the last index, or `false` otherwise.

### Examples

**Example 1:**
```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

**Example 2:**
```
Input: nums = [3,2,1,0,4]
Output: false
```

---

## 🧠 Thought Process

### Key Insight: Greedy 💡
Track the **farthest reachable index**.
- At each step, update max reach
- If current position > max reach, stuck!
- If max reach >= last index, success!

---

## 💡 Solution

```python
def canJump(nums: list[int]) -> bool:
    max_reach = 0
    
    for i in range(len(nums)):
        if i > max_reach:
            return False
        max_reach = max(max_reach, i + nums[i])
    
    return True
```

---

## 🔍 Detailed Walkthrough

```
nums = [2, 3, 1, 1, 4]

i=0: max_reach = max(0, 0+2) = 2
i=1: 1 <= 2 ✓, max_reach = max(2, 1+3) = 4
i=2: 2 <= 4 ✓, max_reach = max(4, 2+1) = 4
i=3: 3 <= 4 ✓, max_reach = max(4, 3+1) = 4
i=4: 4 <= 4 ✓, reached end!

Result: True ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Greedy** - Track farthest reach
2. **Check each position** - Can we get here?
3. **Update max** - i + nums[i]
4. **Early termination** - If stuck

---

## 🔗 Related Problems
- Jump Game II (min jumps)
- Jump Game III
- Jump Game IV
