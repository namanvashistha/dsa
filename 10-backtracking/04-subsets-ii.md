# Subsets II

## 📋 Problem Statement

Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set).

The solution set **must not** contain duplicate subsets.

### Examples

**Example 1:**
```
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

---

## 🧠 Thought Process

### Key Insight 💡
Sort first, then skip duplicates:
- If current == previous AND previous wasn't included → skip
- This avoids duplicate subsets

---

## 💡 Solution

```python
def subsetsWithDup(nums: list[int]) -> list[list[int]]:
    nums.sort()  # Sort to group duplicates
    result = []
    subset = []
    
    def backtrack(i):
        if i == len(nums):
            result.append(subset.copy())
            return
        
        # Include nums[i]
        subset.append(nums[i])
        backtrack(i + 1)
        subset.pop()
        
        # Skip duplicates
        while i + 1 < len(nums) and nums[i] == nums[i + 1]:
            i += 1
        
        # Exclude nums[i]
        backtrack(i + 1)
    
    backtrack(0)
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × 2^n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Sort first** - Group duplicates together
2. **Skip all duplicates** - When not including
3. **Include before skip** - Ensures one copy
4. **Pattern for duplicates** - Sort + skip

---

## 🔗 Related Problems
- Subsets
- Combination Sum II
- Permutations II
