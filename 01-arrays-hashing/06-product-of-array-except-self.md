# Product of Array Except Self

## 📋 Problem Statement

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in **O(n)** time and **without using the division operation**.

### Examples

**Example 1:**
```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
Explanation:
- answer[0] = 2*3*4 = 24
- answer[1] = 1*3*4 = 12
- answer[2] = 1*2*4 = 8
- answer[3] = 1*2*3 = 6
```

**Example 2:**
```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

### Constraints
- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`
- No division allowed
- O(n) time required

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- For each position, multiply all OTHER elements
- Can't use division (otherwise: total_product / nums[i])
- Must be O(n)

### Step 2: The Division Approach (Not Allowed!)
```python
# This is NOT allowed but helps understand
total = 1
for num in nums:
    total *= num
return [total // num for num in nums]  # Division not allowed!
```

### Step 3: Key Insight 💡

For any position `i`:
```
answer[i] = (product of all elements to the LEFT) × (product of all elements to the RIGHT)
```

Example: `nums = [1, 2, 3, 4]`
```
answer[2] (for element 3) = (1 × 2) × (4) = 8
                              ↑          ↑
                           left        right
```

### Step 4: The Strategy
1. **First pass (left to right):** Calculate prefix products
2. **Second pass (right to left):** Multiply by suffix products

---

## 💡 Solution Approaches

### Approach 1: Two Arrays (Prefix + Suffix)

```python
def productExceptSelf(nums: list[int]) -> list[int]:
    n = len(nums)
    
    # prefix[i] = product of all elements to the left of i
    prefix = [1] * n
    for i in range(1, n):
        prefix[i] = prefix[i-1] * nums[i-1]
    
    # suffix[i] = product of all elements to the right of i
    suffix = [1] * n
    for i in range(n-2, -1, -1):
        suffix[i] = suffix[i+1] * nums[i+1]
    
    # answer[i] = prefix[i] * suffix[i]
    answer = [prefix[i] * suffix[i] for i in range(n)]
    
    return answer
```

**Walkthrough:** `nums = [1, 2, 3, 4]`
```
Build prefix (left products):
prefix[0] = 1 (nothing to left)
prefix[1] = prefix[0] × nums[0] = 1 × 1 = 1
prefix[2] = prefix[1] × nums[1] = 1 × 2 = 2
prefix[3] = prefix[2] × nums[2] = 2 × 3 = 6
prefix = [1, 1, 2, 6]

Build suffix (right products):
suffix[3] = 1 (nothing to right)
suffix[2] = suffix[3] × nums[3] = 1 × 4 = 4
suffix[1] = suffix[2] × nums[2] = 4 × 3 = 12
suffix[0] = suffix[1] × nums[1] = 12 × 2 = 24
suffix = [24, 12, 4, 1]

Combine:
answer[0] = 1 × 24 = 24
answer[1] = 1 × 12 = 12
answer[2] = 2 × 4 = 8
answer[3] = 6 × 1 = 6
answer = [24, 12, 8, 6] ✓
```

### Approach 2: O(1) Space (Optimal) ⭐

```python
def productExceptSelf(nums: list[int]) -> list[int]:
    n = len(nums)
    answer = [1] * n
    
    # First pass: left to right (prefix products)
    left_product = 1
    for i in range(n):
        answer[i] = left_product
        left_product *= nums[i]
    
    # Second pass: right to left (multiply by suffix products)
    right_product = 1
    for i in range(n - 1, -1, -1):
        answer[i] *= right_product
        right_product *= nums[i]
    
    return answer
```

**Walkthrough:** `nums = [1, 2, 3, 4]`
```
After first pass (left products stored in answer):
i=0: answer[0]=1, left_product=1×1=1
i=1: answer[1]=1, left_product=1×2=2
i=2: answer[2]=2, left_product=2×3=6
i=3: answer[3]=6, left_product=6×4=24
answer = [1, 1, 2, 6]

After second pass (multiply by right products):
i=3: answer[3]=6×1=6, right_product=1×4=4
i=2: answer[2]=2×4=8, right_product=4×3=12
i=1: answer[1]=1×12=12, right_product=12×2=24
i=0: answer[0]=1×24=24, right_product=24×1=24
answer = [24, 12, 8, 6] ✓
```

---

## 📊 Visualization

```
nums =    [  1,   2,   3,   4  ]
           ↓    ↓    ↓    ↓
prefix =  [  1,   1,   2,   6  ]  (product of elements before)
suffix =  [ 24,  12,   4,   1  ]  (product of elements after)
           ↓    ↓    ↓    ↓
answer =  [ 24,  12,   8,   6  ]  (prefix × suffix)
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Two Arrays | O(n) | O(n) |
| Optimal | O(n) | O(1)* |

*O(1) extra space, not counting output array

---

## 🎯 Key Takeaways

1. **Think in terms of prefix and suffix** - Common pattern!
2. **Two passes solve many problems** - Left-to-right then right-to-left
3. **Use output array for intermediate storage** - Saves space
4. **When division isn't allowed** - Think of breaking down the product

---

## ⚠️ Common Mistakes

1. Starting prefix with nums[0] instead of 1
2. Forgetting the "except self" part
3. Off-by-one errors in indices
4. Not handling zeros correctly

---

## 🔍 Edge Cases

### Handling Zeros
The algorithm handles zeros correctly:
```
nums = [0, 1, 2]
prefix = [1, 0, 0]
suffix = [2, 2, 1]
answer = [2, 0, 0] ✓

nums = [0, 0]
prefix = [1, 0]
suffix = [0, 1]
answer = [0, 0] ✓
```

---

## 🔗 Related Problems
- Trapping Rain Water (also uses prefix/suffix)
- Maximum Product Subarray
- Range Sum Query - Immutable (prefix sums)
