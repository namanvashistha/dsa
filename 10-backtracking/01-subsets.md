# Subsets

## 📋 Problem Statement

Given an integer array `nums` of **unique** elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

### Examples

**Example 1:**
```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**Example 2:**
```
Input: nums = [0]
Output: [[],[0]]
```

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Generate all 2^n subsets
- Each element: include or exclude
- No duplicates (elements are unique)

### Step 2: Backtracking Approach
```
For each element, we have 2 choices:
1. Include it in current subset
2. Exclude it from current subset
```

---

## 💡 Solution

```python
def subsets(nums: list[int]) -> list[list[int]]:
    result = []
    subset = []
    
    def backtrack(i):
        if i == len(nums):
            result.append(subset.copy())
            return
        
        # Include nums[i]
        subset.append(nums[i])
        backtrack(i + 1)
        
        # Exclude nums[i] (backtrack)
        subset.pop()
        backtrack(i + 1)
    
    backtrack(0)
    return result
```

---

## 🔍 Detailed Walkthrough

```
nums = [1, 2, 3]

                     []
                   /    \
           [1]              []
          /   \           /    \
     [1,2]    [1]      [2]      []
     /  \     /  \     /  \    /  \
[1,2,3][1,2][1,3][1] [2,3][2] [3] []

Result: [[1,2,3],[1,2],[1,3],[1],[2,3],[2],[3],[]]
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n × 2^n) |
| Space | O(n) |

2^n subsets, each takes O(n) to copy.

---

## 🎯 Key Takeaways

1. **Include or exclude** - Binary choice at each step
2. **Backtrack = undo choice** - Pop after recursion
3. **Copy subset** - Don't store reference!
4. **Base case** - When index reaches end

---

## 🔗 Related Problems
- Subsets II (with duplicates)
- Combinations
- Permutations
- Combination Sum
