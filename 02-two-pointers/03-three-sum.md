# 3Sum

## 📋 Problem Statement

Given an integer array `nums`, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

### Examples

**Example 1:**
```
Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation: 
nums[0] + nums[1] + nums[2] = -1 + 0 + 1 = 0
nums[1] + nums[2] + nums[4] = 0 + 1 + -1 = 0
nums[0] + nums[3] + nums[4] = -1 + 2 + -1 = 0
The distinct triplets are [-1,0,1] and [-1,-1,2].
```

**Example 2:**
```
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.
```

**Example 3:**
```
Input: nums = [0,0,0]
Output: [[0,0,0]]
```

### Constraints
- `3 <= nums.length <= 3000`
- `-10^5 <= nums[i] <= 10^5`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Find three numbers that sum to 0
- No duplicate triplets in output
- Order within triplet doesn't matter

### Step 2: Key Insight 💡
**3Sum = 1 fixed number + 2Sum!**

```
For each number nums[i]:
  Find two numbers that sum to -nums[i]
```

### Step 3: Handle Duplicates
- Sort the array first
- Skip duplicate values for the fixed number
- Skip duplicate values in Two Pointers

### Step 4: Strategy
1. Sort array
2. Fix first number (iterate)
3. Two Pointers for remaining two numbers
4. Skip duplicates at each level

---

## 💡 Solution

```python
def threeSum(nums: list[int]) -> list[list[int]]:
    nums.sort()
    result = []
    n = len(nums)
    
    for i in range(n - 2):
        # Skip duplicates for first number
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        
        # Early termination: smallest number > 0
        if nums[i] > 0:
            break
        
        # Two pointers for remaining two numbers
        target = -nums[i]
        left = i + 1
        right = n - 1
        
        while left < right:
            current_sum = nums[left] + nums[right]
            
            if current_sum == target:
                result.append([nums[i], nums[left], nums[right]])
                
                # Skip duplicates for second number
                while left < right and nums[left] == nums[left + 1]:
                    left += 1
                # Skip duplicates for third number
                while left < right and nums[right] == nums[right - 1]:
                    right -= 1
                
                left += 1
                right -= 1
            
            elif current_sum < target:
                left += 1
            else:
                right -= 1
    
    return result
```

---

## 🔍 Detailed Walkthrough

### Example: `nums = [-1, 0, 1, 2, -1, -4]`

```
Step 1: Sort
nums = [-4, -1, -1, 0, 1, 2]

Step 2: Fix i=0, nums[i]=-4, target=4
[-4, -1, -1, 0, 1, 2]
  i   L              R
  
  -1 + 2 = 1 < 4 → L++
  -1 + 2 = 1 < 4 → L++
  0 + 2 = 2 < 4 → L++
  1 + 2 = 3 < 4 → L++
  L >= R, done with i=0

Step 3: Fix i=1, nums[i]=-1, target=1
[-4, -1, -1, 0, 1, 2]
      i   L        R

  -1 + 2 = 1 == 1 → Found! [-1, -1, 2]
  Skip duplicate -1, skip duplicate 2
  L++, R--
  
  0 + 1 = 1 == 1 → Found! [-1, 0, 1]
  L++, R--
  
  L >= R, done with i=1

Step 4: Fix i=2, nums[i]=-1
  Same as nums[i-1], SKIP!

Step 5: Fix i=3, nums[i]=0, target=0
[-4, -1, -1, 0, 1, 2]
            i  L  R

  1 + 2 = 3 > 0 → R--
  L >= R, done with i=3

Step 6: i=4, only 2 elements left, done

Result: [[-1, -1, 2], [-1, 0, 1]] ✓
```

---

## 📊 Visual: Duplicate Skipping

```
Sorted: [-2, -2, -1, -1, 0, 0, 1, 1, 2, 2]

Level 1 (i loop):
  ✓ Process -2 at index 0
  ✗ Skip -2 at index 1 (duplicate)
  ✓ Process -1 at index 2
  ✗ Skip -1 at index 3 (duplicate)
  ... and so on

Level 2 (Two Pointers):
  After finding valid triplet, skip duplicates before moving pointers
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n²) |
| Space | O(1) or O(n)* |

*Sorting might use O(n) space depending on implementation*

- O(n log n) for sorting
- O(n) for each fixed number × O(n) for Two Pointers = O(n²)
- Total: O(n²)

---

## 🎯 Key Takeaways

1. **3Sum = Fix one + 2Sum** - Reduce problem dimension
2. **Sort first** - Enables Two Pointers and duplicate skipping
3. **Skip duplicates at all levels** - Critical for unique triplets
4. **Early termination** - If smallest > 0, no solution possible

---

## ⚠️ Common Mistakes

1. Not sorting the array first
2. Forgetting to skip duplicates at any level
3. Wrong duplicate skipping logic (checking wrong indices)
4. Not handling all-zeros case correctly

---

## 🔄 Duplicate Skipping Logic

```python
# For first number (i loop)
if i > 0 and nums[i] == nums[i - 1]:
    continue

# For second number (after finding triplet)
while left < right and nums[left] == nums[left + 1]:
    left += 1

# For third number (after finding triplet)
while left < right and nums[right] == nums[right - 1]:
    right -= 1

# Then move both pointers
left += 1
right -= 1
```

---

## 🧪 Edge Cases

```python
# All same positive
nums = [1, 1, 1]  # Output: []

# All zeros
nums = [0, 0, 0]  # Output: [[0, 0, 0]]

# No valid triplet
nums = [1, 2, 3]  # Output: []

# Many duplicates
nums = [-1, -1, -1, 2, 2]  # Output: [[-1, -1, 2]]
```

---

## 🔗 Related Problems
- Two Sum
- Two Sum II - Sorted
- 4Sum
- 3Sum Closest
- 3Sum Smaller
