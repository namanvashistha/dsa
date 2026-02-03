# 📦 Arrays & Hashing - NeetCode 150

> 9 problems | Master frequency counting, HashMaps, and array manipulation

---

## 1️⃣ Contains Duplicate ⭐ Easy
**The Trick:** Just use a HashSet!
- Loop through array, add each number to set
- If number already in set → return true
- **Remember:** `if num in seen: return true`

---

## 2️⃣ Valid Anagram ⭐ Easy
**The Trick:** Count letters in both strings
- Count frequency of each character
- **Quick way:** `sorted(s1) == sorted(s2)`
- **Remember:** Same character counts = anagram

---

## 3️⃣ Two Sum ⭐ Easy
**The Trick:** HashMap stores what you're looking for
- Store `{target - num: index}` in HashMap
- For each num, check if it exists in map
- **Remember:** `map[target - num]` → found it!

---

## 4️⃣ Group Anagrams ⭐⭐ Medium
**The Trick:** Sorted string = anagram key
- Sort each word → use as HashMap key
- **Example:** "eat", "tea", "ate" → all become "aet"
- **Remember:** `map[sorted(word)].append(word)`

---

## 5️⃣ Top K Frequent Elements ⭐⭐ Medium
**The Trick:** Count first, then sort by frequency
- Count frequencies with HashMap
- Use heap (size k) OR bucket sort
- **Lazy approach:** Count → sort → take first k
- **Remember:** Frequency first, then pick top k

---

## 6️⃣ Product of Array Except Self ⭐⭐ Medium
**The Trick:** Left products × Right products
- Pass 1: Product of all elements to the left
- Pass 2: Multiply by product of all to the right
- **No division needed!**
- **Remember:** Two passes, one left one right

---

## 7️⃣ Valid Sudoku ⭐⭐ Medium
**The Trick:** Three HashSets (rows, cols, boxes)
- Track seen in each row (9 sets)
- Track seen in each col (9 sets)
- Track seen in each 3×3 box (9 sets)
- **Box index:** `(row // 3) * 3 + (col // 3)`
- **Remember:** Check 3 things at once

---

## 8️⃣ Encode and Decode Strings ⭐⭐ Medium
**The Trick:** Length prefix: `"4#word"`
- Encode: `len(str) + "#" + str`
- Decode: Read length, read "#", read chars
- **Example:** `["hello"]` → `"5#hello"`
- **Remember:** Length tells where string ends

---

## 9️⃣ Longest Consecutive Sequence ⭐⭐ Medium
**The Trick:** Only start from sequence beginnings
- Put all numbers in HashSet
- For each num, check if `num-1` exists
- If not → sequence start, count up
- **Remember:** `if (num-1) not in set: start counting`

---

## 🎯 Pattern Recognition

**Use HashMap when:**
- Finding duplicates or frequencies
- Need O(1) lookup
- Counting occurrences

**Key Patterns:**
- Anagrams → sort or count characters
- Duplicates → HashSet
- Two sum variants → store complement
- Grouping → use key to identify groups

**Common Mistakes:**
- Forgetting to handle empty inputs
- Not considering duplicate keys
- Using array when HashMap is better
