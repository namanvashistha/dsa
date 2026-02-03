# Combination Sum II

## 📋 Problem Statement

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

### Examples

**Example 1:**
```
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: [[1,1,6],[1,2,5],[1,7],[2,6]]
```

---

## 💡 Solution

```python
def combinationSum2(candidates: list[int], target: int) -> list[list[int]]:
    candidates.sort()
    result = []
    
    def backtrack(start, path, remaining):
        if remaining == 0:
            result.append(path.copy())
            return
        if remaining < 0:
            return
        
        for i in range(start, len(candidates)):
            # Skip duplicates
            if i > start and candidates[i] == candidates[i - 1]:
                continue
            
            path.append(candidates[i])
            backtrack(i + 1, path, remaining - candidates[i])
            path.pop()
    
    backtrack(0, [], target)
    return result
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(2^n) |
| Space | O(n) |

---

## 🎯 Key Takeaways

1. **Sort + skip duplicates** - At same level
2. **i > start** - Allow same value at different levels
3. **i + 1** - Each element used once
4. **Combination Sum variant** - No reuse

---

## 🔗 Related Problems
- Combination Sum
- Combination Sum III
