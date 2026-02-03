# Combination Sum

## 📋 Problem Statement

Given an array of **distinct** integers `candidates` and a target integer `target`, return a list of all **unique combinations** of candidates where the chosen numbers sum to target. You may return the combinations in any order.

The **same** number may be chosen from candidates an **unlimited number of times**.

### Examples

**Example 1:**
```
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
```

**Example 2:**
```
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]
```

---

## 🧠 Thought Process

### Key Insight 💡
Backtracking with:
- Can reuse same element (don't increment index)
- Target decreases with each choice
- Stop when target = 0 or negative

---

## 💡 Solution

```python
def combinationSum(candidates: list[int], target: int) -> list[list[int]]:
    result = []
    
    def backtrack(start, path, remaining):
        if remaining == 0:
            result.append(path.copy())
            return
        if remaining < 0:
            return
        
        for i in range(start, len(candidates)):
            path.append(candidates[i])
            backtrack(i, path, remaining - candidates[i])  # Same i (can reuse)
            path.pop()
    
    backtrack(0, [], target)
    return result
```

---

## 🔍 Detailed Walkthrough

```
candidates = [2,3,6,7], target = 7

backtrack(0, [], 7)
  Try 2: backtrack(0, [2], 5)
    Try 2: backtrack(0, [2,2], 3)
      Try 2: backtrack(0, [2,2,2], 1)
        Try 2: remaining -1 → return
        Try 3: remaining -2 → return
      Try 3: backtrack(0, [2,2,3], 0) → Add [2,2,3] ✓
    Try 3: backtrack(1, [2,3], 2)
      ... not fruitful
  Try 3: ...
  Try 7: backtrack(3, [7], 0) → Add [7] ✓

Result: [[2,2,3], [7]] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n^(t/m)) |
| Space | O(t/m) |

Where t = target, m = min candidate

---

## 🎯 Key Takeaways

1. **Same index for reuse** - Don't increment i
2. **Start index** - Avoid duplicates like [2,3] and [3,2]
3. **Early termination** - When remaining < 0

---

## 🔗 Related Problems
- Combination Sum II (no reuse, duplicates)
- Combination Sum III
- Coin Change
