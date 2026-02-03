# Permutations

## 📋 Problem Statement

Given an array `nums` of distinct integers, return all the possible permutations. You can return the answer in any order.

### Examples

**Example 1:**
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

**Example 2:**
```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Generate all n! permutations
- Each element used exactly once
- Order matters

### Step 2: Backtracking Approach
At each position, try all unused elements.

---

## 💡 Solution

```python
def permute(nums: list[int]) -> list[list[int]]:
    result = []
    path = []
    used = [False] * len(nums)
    
    def backtrack():
        if len(path) == len(nums):
            result.append(path.copy())
            return
        
        for i in range(len(nums)):
            if used[i]:
                continue
            
            # Choose
            path.append(nums[i])
            used[i] = True
            
            # Explore
            backtrack()
            
            # Unchoose (backtrack)
            path.pop()
            used[i] = False
    
    backtrack()
    return result
```

---

## 🔍 Detailed Walkthrough

```
nums = [1, 2, 3]

Start: path=[]
  Try 1: path=[1], used=[T,F,F]
    Try 2: path=[1,2], used=[T,T,F]
      Try 3: path=[1,2,3] → add to result!
      Backtrack: path=[1,2]
    Backtrack: path=[1]
    Try 3: path=[1,3], used=[T,F,T]
      Try 2: path=[1,3,2] → add to result!
      ...
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n! × n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Track used elements** - Boolean array or set
2. **Try all unused at each position** - The key pattern
3. **Backtrack = unmark and remove** - Restore state
4. **Base case** - Path length equals nums length

---

## 🔗 Related Problems
- Permutations II (with duplicates)
- Next Permutation
- Permutation Sequence
