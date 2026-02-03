# Two Sum

## 📋 Problem Statement

Given an array of integers `nums` and an integer `target`, return **indices** of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

You can return the answer in any order.

### Examples

**Example 1:**
```
Input: nums = [2, 7, 11, 15], target = 9
Output: [0, 1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

**Example 2:**
```
Input: nums = [3, 2, 4], target = 6
Output: [1, 2]
Explanation: nums[1] + nums[2] = 2 + 4 = 6
```

**Example 3:**
```
Input: nums = [3, 3], target = 6
Output: [0, 1]
```

### Constraints
- `2 <= nums.length <= 10^4`
- `-10^9 <= nums[i] <= 10^9`
- `-10^9 <= target <= 10^9`
- **Only one valid answer exists**

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find TWO numbers that sum to target
- Return their INDICES (not values)
- Exactly one solution exists
- Can't use same element twice

### Step 2: Brute Force Thinking
- Check every pair of numbers
- Time: O(n²)
- Can we do better?

### Step 3: Key Insight 💡
If we're looking at number `x`, we need `target - x` to exist.

**Question:** How can we quickly check if `target - x` exists?
**Answer:** HashMap! Store numbers we've seen with their indices.

### Step 4: The Trick
For each number `num`:
1. Calculate complement: `complement = target - num`
2. Check if complement exists in HashMap
3. If yes → found the pair!
4. If no → store current number in HashMap for future lookups

---

## 💡 Solution Approaches

### Approach 1: Brute Force

```python
def twoSum(nums: list[int], target: int) -> list[int]:
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
    
    return []  # No solution found
```

### Approach 2: HashMap - One Pass (Optimal)

```python
def twoSum(nums: list[int], target: int) -> list[int]:
    seen = {}  # value -> index
    
    for i, num in enumerate(nums):
        complement = target - num
        
        if complement in seen:
            return [seen[complement], i]
        
        seen[num] = i
    
    return []
```

**Walkthrough with Example:** `nums = [2, 7, 11, 15], target = 9`
```
Step 1: i=0, num=2
        complement = 9 - 2 = 7
        7 not in seen (seen is empty)
        Add to seen: seen = {2: 0}

Step 2: i=1, num=7
        complement = 9 - 7 = 2
        2 IS in seen! seen[2] = 0
        Return [0, 1] ✓
```

### Approach 3: HashMap - Two Pass

```python
def twoSum(nums: list[int], target: int) -> list[int]:
    # Pass 1: Build HashMap
    num_to_index = {}
    for i, num in enumerate(nums):
        num_to_index[num] = i
    
    # Pass 2: Find complement
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_to_index and num_to_index[complement] != i:
            return [i, num_to_index[complement]]
    
    return []
```

**Note:** The check `num_to_index[complement] != i` ensures we don't use the same element twice.

---

## 🔍 Why One-Pass Works

In the one-pass approach, we might wonder: "What if the complement comes AFTER the current number?"

**Answer:** When we reach the complement later, the current number will already be in the HashMap!

Example: `nums = [3, 2, 4], target = 6`
- When we're at 2 (index 1), we look for 4 → not found yet
- When we're at 4 (index 2), we look for 2 → found at index 1!

The pair will always be found when we reach the SECOND number of the pair.

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Brute Force | O(n²) | O(1) |
| HashMap One-Pass | O(n) | O(n) |
| HashMap Two-Pass | O(n) | O(n) |

---

## 🎯 Key Takeaways

1. **HashMap for complement lookup** - Classic pattern!
2. **Think about what you're searching for** - If looking for X, store X for quick lookup
3. **One-pass vs Two-pass** - One-pass is elegant but two-pass is clearer
4. **Store index, not just existence** - Problem asks for indices

---

## ⚠️ Common Mistakes

1. Returning values instead of indices
2. Using same element twice (e.g., [3] with target 6)
3. Not handling duplicates (e.g., [3, 3] with target 6)

---

## 🔄 Variations

### What if array is sorted?
Use **Two Pointers** instead! O(1) space, O(n) time.

```python
def twoSumSorted(nums: list[int], target: int) -> list[int]:
    left, right = 0, len(nums) - 1
    
    while left < right:
        current_sum = nums[left] + nums[right]
        
        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1
        else:
            right -= 1
    
    return []
```

---

## 🔗 Related Problems
- Two Sum II - Input Array Is Sorted (Two Pointers)
- 3Sum (Fix one, two sum for rest)
- 4Sum
- Two Sum III - Data Structure Design
