# Merge Triplets to Form Target Triplet

## 📋 Problem Statement

A triplet is an array of three integers. You are given a 2D integer array `triplets` and an integer array `target`.

To get `target`, you can apply any number of the following operation:
- Choose two different triplets and update each value in one triplet to be the maximum of corresponding values.

Return `true` if it is possible to obtain the `target` triplet as an element of `triplets` after any number of operations.

### Examples

**Example 1:**
```
Input: triplets = [[2,5,3],[1,8,4],[1,7,5]], target = [2,7,5]
Output: true
Explanation: Use [2,5,3] and [1,7,5] → max values give [2,7,5]
```

---

## 🧠 Thought Process

### Key Insight 💡
- Can't use triplet if ANY value exceeds target
- For each valid triplet, check which target values it provides
- Need to find all three target values

---

## 💡 Solution

```python
def mergeTriplets(triplets: list[list[int]], target: list[int]) -> bool:
    good = set()
    
    for triplet in triplets:
        # Skip if any value exceeds target
        if (triplet[0] > target[0] or 
            triplet[1] > target[1] or 
            triplet[2] > target[2]):
            continue
        
        # Check which target values this triplet can provide
        for i in range(3):
            if triplet[i] == target[i]:
                good.add(i)
    
    return len(good) == 3
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Filter invalid triplets** - Any value > target
2. **Collect matching positions** - Which indices match target
3. **Need all three** - Can merge multiple valid triplets
4. **Max operation** - Can only increase values

---

## 🔗 Related Problems
- Maximum of Minimum Values in All Subarrays
