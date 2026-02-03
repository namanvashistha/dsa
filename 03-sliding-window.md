# 🪟 Sliding Window - NeetCode 150

> 6 problems | Master dynamic window expansion and contraction

---

## 1️⃣ Best Time to Buy and Sell Stock ⭐ Easy
**The Trick:** Track minimum price, update max profit
- Keep lowest price seen so far
- Calculate profit if sold today
- Update max profit
- **Remember:** Buy at min, sell at current

---

## 2️⃣ Longest Substring Without Repeating ⭐⭐ Medium
**The Trick:** Expand right, shrink left on duplicate
- Use HashSet to track chars in window
- Expand right pointer
- Duplicate found → shrink left until no duplicate
- **Remember:** Sliding window + HashSet

---

## 3️⃣ Longest Repeating Character Replacement ⭐⭐ Medium
**The Trick:** Valid if `windowSize - maxFreq ≤ k`
- Count char frequencies in window
- Track most frequent char count
- Can replace `windowSize - maxFreq` characters
- If ≤ k → valid window!
- **Remember:** Replace the minority characters

---

## 4️⃣ Permutation in String ⭐⭐ Medium
**The Trick:** Fixed-size window + char count
- Window size = length of s1
- Slide window across s2
- Compare character frequencies
- **Remember:** Permutation = same char counts

---

## 5️⃣ Minimum Window Substring ⭐⭐⭐ Hard
**The Trick:** Expand until valid, then shrink
- Expand right until contains all chars of t
- Shrink left while still valid, record min
- Keep expanding and shrinking
- **Remember:** Expand → shrink → repeat

---

## 6️⃣ Sliding Window Maximum ⭐⭐⭐ Hard
**The Trick:** Monotonic decreasing deque
- Store indices in deque, not values
- Keep deque decreasing (remove smaller from back)
- Remove out-of-window indices from front
- Front of deque = max of current window
- **Remember:** Deque stores indices in decreasing order

---

## 🎯 Pattern Recognition

**Use Sliding Window when:**
- Subarray/substring problems
- Contiguous elements
- "Longest/shortest/max/min" with condition

**Two Types:**
1. **Fixed Size:** Window size is constant (e.g., size k)
   - Move both pointers together
   
2. **Variable Size:** Window grows/shrinks based on condition
   - Expand right to find candidate
   - Shrink left to optimize

**Common Patterns:**
- "Longest substring with..." → variable window
- "All subarrays of size k" → fixed window
- Use HashMap/Set to track window contents

**Template:**
```
left = 0
for right in range(len(array)):
    add array[right] to window
    
    while window invalid:
        remove array[left] from window
        left += 1
    
    update result
```

**Common Mistakes:**
- Not updating window state when shrinking
- Off-by-one errors in window size
- Forgetting to track window contents
