# Longest Consecutive Sequence

## 📋 Problem Statement

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in **O(n)** time.

### Examples

**Example 1:**
```
Input: nums = [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive sequence is [1, 2, 3, 4]. Length = 4.
```

**Example 2:**
```
Input: nums = [0, 3, 7, 2, 5, 8, 4, 6, 0, 1]
Output: 9
Explanation: The longest consecutive sequence is [0, 1, 2, 3, 4, 5, 6, 7, 8]. Length = 9.
```

### Constraints
- `0 <= nums.length <= 10^5`
- `-10^9 <= nums[i] <= 10^9`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find longest sequence of consecutive integers
- Array is UNSORTED
- Must be O(n) time (can't sort!)

### Step 2: Brute Force (Too Slow)
```python
# O(n³) approach - for each number, check consecutive sequence
for num in nums:
    count = 1
    while num + count in nums:  # O(n) per check
        count += 1
```

### Step 3: Key Insight 💡
**Only start counting from sequence BEGINNINGS!**

A number is a sequence start if `num - 1` is NOT in the array.

```
nums = [100, 4, 200, 1, 3, 2]

1 is a start (0 not in nums)
2 is NOT a start (1 is in nums)
3 is NOT a start (2 is in nums)
4 is NOT a start (3 is in nums)
100 is a start (99 not in nums)
200 is a start (199 not in nums)

Only count from: 1, 100, 200
```

### Step 4: Why This is O(n)
- We only iterate from sequence starts
- Each number is visited at most twice:
  1. Once when checking if it's a start
  2. Once when counting from another start
- Total: O(n)

---

## 💡 Solution

```python
def longestConsecutive(nums: list[int]) -> int:
    if not nums:
        return 0
    
    num_set = set(nums)  # O(1) lookup
    longest = 0
    
    for num in num_set:
        # Only start counting if this is the START of a sequence
        if num - 1 not in num_set:
            current_num = num
            current_length = 1
            
            # Count consecutive numbers
            while current_num + 1 in num_set:
                current_num += 1
                current_length += 1
            
            longest = max(longest, current_length)
    
    return longest
```

---

## 🔍 Detailed Walkthrough

### Example: `nums = [100, 4, 200, 1, 3, 2]`

```
Step 1: Create set
num_set = {100, 4, 200, 1, 3, 2}

Step 2: Process each number

num = 100:
  Is 99 in set? No → sequence start!
  Count: 100, check 101? No
  Length: 1
  longest = 1

num = 4:
  Is 3 in set? Yes → NOT a start, skip

num = 200:
  Is 199 in set? No → sequence start!
  Count: 200, check 201? No
  Length: 1
  longest = max(1, 1) = 1

num = 1:
  Is 0 in set? No → sequence start!
  Count: 1, check 2? Yes!
  Count: 2, check 3? Yes!
  Count: 3, check 4? Yes!
  Count: 4, check 5? No
  Length: 4
  longest = max(1, 4) = 4

num = 3:
  Is 2 in set? Yes → NOT a start, skip

num = 2:
  Is 1 in set? Yes → NOT a start, skip

Final: longest = 4 ✓
```

---

## 📊 Visual Representation

```
nums = [100, 4, 200, 1, 3, 2]

Number Line:
... 1--2--3--4 ... 100 ... 200 ...
    [  seq 1  ]    [2]    [3]

Sequence 1: [1, 2, 3, 4] → length 4 ⭐ longest
Sequence 2: [100] → length 1
Sequence 3: [200] → length 1
```

---

## 📊 Complexity Analysis

| Step | Time | Space |
|------|------|-------|
| Build Set | O(n) | O(n) |
| Find Sequences | O(n)* | O(1) |
| **Total** | **O(n)** | **O(n)** |

*Each element visited at most twice

---

## 🔍 Why It's Really O(n)

The key concern: "Aren't we doing O(n) work in the while loop for each start?"

**Answer:** No! Consider all the while loop iterations across ALL starts:
- Each number is counted exactly ONCE (only from its sequence start)
- Total while loop iterations = total numbers in all sequences = n

Example:
```
nums = [1, 2, 3, 4, 100, 200]

From 1: count 1, 2, 3, 4 (4 iterations)
From 100: count 100 (1 iteration)
From 200: count 200 (1 iteration)

Total iterations: 4 + 1 + 1 = 6 = n
```

---

## 🎯 Key Takeaways

1. **Start from sequence beginnings** - Avoid counting subsequences
2. **HashSet for O(1) lookup** - Essential for efficiency
3. **Amortized analysis** - While loops across all iterations still O(n)
4. **"Is predecessor present?"** - Key check for identifying starts

---

## ⚠️ Common Mistakes

1. Sorting the array (violates O(n) requirement)
2. Starting count from every number (leads to redundant work)
3. Not using set (O(n) lookup in list)
4. Forgetting to handle empty array

---

## 🔄 Alternative: Union-Find

```python
def longestConsecutive(nums: list[int]) -> int:
    if not nums:
        return 0
    
    num_set = set(nums)
    parent = {num: num for num in nums}
    size = {num: 1 for num in nums}
    
    def find(x):
        if parent[x] != x:
            parent[x] = find(parent[x])
        return parent[x]
    
    def union(x, y):
        px, py = find(x), find(y)
        if px == py:
            return
        if size[px] < size[py]:
            px, py = py, px
        parent[py] = px
        size[px] += size[py]
    
    for num in num_set:
        if num + 1 in num_set:
            union(num, num + 1)
    
    return max(size.values())
```

This is also O(n) with inverse Ackermann factor, but more complex.

---

## 🔗 Related Problems
- Longest Substring Without Repeating Characters
- Binary Tree Longest Consecutive Sequence
- Find the Duplicate Number
- Missing Number
