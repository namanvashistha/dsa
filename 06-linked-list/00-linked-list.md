# 🔗 Linked List - NeetCode 150

> 11 problems | Master pointer manipulation and list traversal

---

## 1️⃣ Reverse Linked List ⭐ Easy
**The Trick:** Three pointers (prev, curr, next)
- Save next: `next = curr.next`
- Reverse: `curr.next = prev`
- Move: `prev = curr; curr = next`
- **Remember:** prev → null initially, return prev at end

---

## 2️⃣ Merge Two Sorted Lists ⭐ Easy
**The Trick:** Dummy node + compare and link
- Create dummy node to simplify edge cases
- Compare heads, link smaller
- Move pointer forward
- **Remember:** Dummy node trick for easy return

---

## 3️⃣ Reorder List ⭐⭐ Medium
**The Trick:** Find middle → reverse second half → merge
- Step 1: Find middle (slow/fast pointers)
- Step 2: Reverse second half
- Step 3: Merge alternating from both halves
- **Remember:** Three separate operations combined

---

## 4️⃣ Remove Nth Node From End ⭐⭐ Medium
**The Trick:** Two pointers with n gap
- Fast pointer moves n steps ahead
- Move both until fast reaches end
- Slow is at (n-1)th from end
- **Remember:** Use dummy node for edge cases

---

## 5️⃣ Copy List with Random Pointer ⭐⭐ Medium
**The Trick:** HashMap or interweaving nodes
- **HashMap:** Map old → new, then set next/random
- **Interweave:** A→A'→B→B', then separate
- **Remember:** Create all nodes first, then set pointers

---

## 6️⃣ Add Two Numbers ⭐⭐ Medium
**The Trick:** Traverse and add with carry
- Add corresponding digits + carry
- Create new node with `sum % 10`
- Carry = `sum // 10`
- **Remember:** Don't forget final carry

---

## 7️⃣ Linked List Cycle ⭐ Easy
**The Trick:** Fast and slow pointers (Floyd's)
- Slow moves 1 step, fast moves 2 steps
- If they meet → cycle exists
- If fast reaches null → no cycle
- **Remember:** Tortoise and hare

---

## 8️⃣ Find Duplicate Number ⭐⭐ Medium
**The Trick:** Floyd's cycle detection in array
- Treat array as linked list: `next = nums[curr]`
- Find intersection (cycle exists)
- Find cycle start = duplicate
- **Remember:** Array indices as pointers

---

## 9️⃣ LRU Cache ⭐⭐ Medium
**The Trick:** HashMap + Doubly Linked List
- HashMap for O(1) access
- DLL for O(1) removal/addition
- Most recent at head, LRU at tail
- **Remember:** HashMap points to DLL nodes

---

## 🔟 Merge K Sorted Lists ⭐⭐⭐ Hard
**The Trick:** Min heap or divide & conquer
- **Heap:** Add all heads, pop min, add next
- **D&C:** Merge pairs recursively
- **Remember:** Heap with (value, list_index)

---

## 1️⃣1️⃣ Reverse Nodes in K-Group ⭐⭐⭐ Hard
**The Trick:** Check length, reverse in groups
- Check if k nodes remaining
- Reverse k nodes
- Connect with previous group
- Recursively process rest
- **Remember:** Check length first, then reverse

---

## 🎯 Pattern Recognition

**Use Linked List patterns:**
- **Dummy Node:** Simplifies edge cases (head changes)
- **Two Pointers:** Fast/slow, different speeds
- **Reverse:** Three pointers (prev, curr, next)
- **HashMap:** For O(1) lookup with nodes

**Common Techniques:**

1. **Fast & Slow Pointers:**
   - Find middle: slow moves 1, fast moves 2
   - Detect cycle: if they meet
   
2. **Dummy Node:**
   - When head might change
   - Simplifies merge operations
   
3. **Recursion:**
   - Natural for linked lists
   - Base case: null or single node

**Key Operations:**
```python
# Reverse
prev, curr = None, head
while curr:
    next = curr.next
    curr.next = prev
    prev, curr = curr, next

# Find middle
slow = fast = head
while fast and fast.next:
    slow = slow.next
    fast = fast.next.next
```

**Common Mistakes:**
- Losing reference to next node before changing pointers
- Not using dummy node when head changes
- Forgetting null checks
- Off-by-one in counting

**Key Insight:**
- Draw it out! Linked list problems are visual
- Always consider: empty list, single node, two nodes
