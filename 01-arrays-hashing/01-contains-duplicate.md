# Contains Duplicate

## 📋 Problem Statement

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

### Examples

**Example 1:**
```
Input: nums = [1, 2, 3, 1]
Output: true
Explanation: 1 appears twice
```

**Example 2:**
```
Input: nums = [1, 2, 3, 4]
Output: false
Explanation: All elements are distinct
```

**Example 3:**
```
Input: nums = [1, 1, 1, 3, 3, 4, 3, 2, 4, 2]
Output: true
```

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- We need to find if ANY element appears more than once
- We don't need to know which element or how many times
- Just a simple yes/no (true/false) answer

### Step 2: Consider Brute Force
- Compare every element with every other element
- Time: O(n²) - nested loops
- Space: O(1)
- **Too slow for large inputs!**

### Step 3: Think About Optimization
**Key Insight:** How can we quickly check if we've seen a number before?

Options:
1. **Sorting:** Sort array, duplicates will be adjacent → O(n log n)
2. **HashSet:** Store seen numbers, O(1) lookup → O(n)

### Step 4: Choose Best Approach
HashSet is optimal:
- We iterate once through array
- For each number, check if already in set
- If yes → duplicate found, return True
- If no → add to set, continue

---

## 💡 Solution Approaches

### Approach 1: HashSet (Optimal)

```python
def containsDuplicate(nums: list[int]) -> bool:
    seen = set()
    
    for num in nums:
        if num in seen:
            return True
        seen.add(num)
    
    return False
```

**Walkthrough with Example:** `nums = [1, 2, 3, 1]`
```
Step 1: num=1, seen={}, 1 not in seen → add 1, seen={1}
Step 2: num=2, seen={1}, 2 not in seen → add 2, seen={1,2}
Step 3: num=3, seen={1,2}, 3 not in seen → add 3, seen={1,2,3}
Step 4: num=1, seen={1,2,3}, 1 IS in seen → return True ✓
```

### Approach 2: One-liner with Set Length

```python
def containsDuplicate(nums: list[int]) -> bool:
    return len(nums) != len(set(nums))
```

**Logic:** If there are duplicates, the set (unique elements) will be smaller than original array.

### Approach 3: Sorting

```python
def containsDuplicate(nums: list[int]) -> bool:
    nums.sort()
    
    for i in range(1, len(nums)):
        if nums[i] == nums[i - 1]:
            return True
    
    return False
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| HashSet (iterative) | O(n) | O(n) |
| Set length | O(n) | O(n) |
| Sorting | O(n log n) | O(1)* |

*Sorting is O(1) extra space if done in-place, but modifies input

---

## 🎯 Key Takeaways

1. **HashSet for O(1) lookup** - When you need to quickly check "have I seen this before?"
2. **Trade space for time** - Using O(n) space gives us O(n) time instead of O(n²)
3. **Set properties** - Sets automatically handle uniqueness

---

## 🔗 Related Problems
- Two Sum (uses HashMap similarly)
- Valid Anagram (counting with HashMap)
- Intersection of Two Arrays
