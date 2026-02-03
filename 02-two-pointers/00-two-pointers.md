# 👉👈 Two Pointers - NeetCode 150

> 5 problems | Master pointer movement strategies

---

## 1️⃣ Valid Palindrome ⭐ Easy
**The Trick:** Compare from both ends
- Left at start, right at end
- Skip non-alphanumeric characters
- Move inward comparing
- **Remember:** Two pointers moving toward each other

---

## 2️⃣ Two Sum II (Sorted Array) ⭐⭐ Medium
**The Trick:** Array is sorted → use two pointers!
- Left at start, right at end
- Sum too small? → move left right
- Sum too big? → move right left
- **Remember:** Sorted = two pointers, not HashMap

---

## 3️⃣ 3Sum ⭐⭐ Medium
**The Trick:** Fix one number, two sum for rest
- Sort array first
- Fix first number, use two pointers for other two
- Skip duplicates for unique triplets
- **Remember:** 3Sum = loop + 2Sum pattern

---

## 4️⃣ Container With Most Water ⭐⭐ Medium
**The Trick:** Always move the shorter line
- Pointers at both ends
- Area = `min(height[left], height[right]) × width`
- Move shorter pointer (might find taller)
- **Remember:** Move shorter pointer inward

---

## 5️⃣ Trapping Rain Water ⭐⭐⭐ Hard
**The Trick:** Water level = min(max_left, max_right)
- Two pointers from both ends
- Track max_left and max_right
- Move pointer with smaller max
- Water trapped = `min(max_left, max_right) - height[i]`
- **Remember:** Move from side with lower max

---

## 🎯 Pattern Recognition

**Use Two Pointers when:**
- Array is sorted
- Finding pairs/triplets
- Comparing from both ends
- Optimizing brute force O(n²) to O(n)

**Movement Strategies:**
- **Opposite direction:** Start from both ends, move toward center
- **Same direction:** Both move left to right (fast & slow)
- **Conditional:** Move based on comparison result

**Key Decision:**
- If sorted → definitely try two pointers first
- If need to check all pairs → two pointers if possible

**Common Mistakes:**
- Forgetting to skip duplicates
- Not handling edge cases (empty, single element)
- Wrong pointer movement condition
