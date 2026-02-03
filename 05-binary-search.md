# 🔍 Binary Search - NeetCode 150

> 7 problems | Master search in sorted space and binary search variations

---

## 1️⃣ Binary Search ⭐ Easy
**The Trick:** Eliminate half each iteration
- Compare mid with target
- Target smaller → search left half
- Target larger → search right half
- **Remember:** `left = mid + 1` or `right = mid - 1`

---

## 2️⃣ Search a 2D Matrix ⭐⭐ Medium
**The Trick:** Treat 2D as 1D sorted array
- Binary search on rows first OR
- Convert 2D index to 1D: `mid → [mid//cols][mid%cols]`
- **Remember:** 2D matrix = flattened 1D array

---

## 3️⃣ Koko Eating Bananas ⭐⭐ Medium
**The Trick:** Binary search on answer (eating speed)
- Search range: 1 to max(piles)
- For each speed, check if can finish in h hours
- Find minimum valid speed
- **Remember:** Binary search on the answer, not input

---

## 4️⃣ Find Minimum in Rotated Sorted Array ⭐⭐ Medium
**The Trick:** Compare mid with right boundary
- If `arr[mid] > arr[right]` → min in right half
- Else → min in left half (including mid)
- **Remember:** Compare with right, not left

---

## 5️⃣ Search in Rotated Sorted Array ⭐⭐ Medium
**The Trick:** Find which half is sorted first
- Check if left half sorted: `arr[left] ≤ arr[mid]`
- Check if target in sorted half
- Eliminate one half
- **Remember:** Identify sorted half, check if target there

---

## 6️⃣ Time Based Key-Value Store ⭐⭐ Medium
**The Trick:** Store with timestamp, binary search on time
- Store `[(timestamp, value)]` for each key
- Binary search for largest timestamp ≤ given
- **Remember:** Find rightmost valid timestamp

---

## 7️⃣ Median of Two Sorted Arrays ⭐⭐⭐ Hard
**The Trick:** Binary search on partition point
- Partition smaller array (binary search)
- Ensure left half size = right half size
- Check if partitions valid: `maxLeft ≤ minRight`
- **Remember:** Binary search on smaller array partition

---

## 🎯 Pattern Recognition

**Use Binary Search when:**
- Array is sorted (or rotated sorted)
- Search space has monotonic property
- Need O(log n) instead of O(n)
- "Find minimum/maximum satisfying condition"

**Three Types:**

1. **Classic Binary Search:** Find exact target
   - Sorted array, find element
   
2. **Binary Search on Answer:** Search solution space
   - "Minimum speed", "minimum time"
   - Check if answer valid → binary search
   
3. **Rotated/Modified:** Variations
   - Rotated arrays
   - 2D matrices
   - Finding boundaries

**Template (leftmost/rightmost):**
```
# Find leftmost position
left, right = 0, len(arr)
while left < right:
    mid = (left + right) // 2
    if arr[mid] < target:
        left = mid + 1
    else:
        right = mid
return left

# Find rightmost position
left, right = 0, len(arr)
while left < right:
    mid = (left + right) // 2
    if arr[mid] <= target:
        left = mid + 1
    else:
        right = mid
return left - 1
```

**Common Mistakes:**
- Infinite loop: use `right = mid - 1` or `left = mid + 1`
- Wrong mid calculation (use `left + (right - left) // 2` for safety)
- Off-by-one errors in boundaries
- Not considering edge cases (empty, single element)

**Key Insight:**
- Binary search works on **monotonic functions**
- If you can check "is this answer valid?" in O(n) or less
- Then binary search the answer space!
