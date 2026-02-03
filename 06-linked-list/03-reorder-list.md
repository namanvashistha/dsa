# Reorder List

## 📋 Problem Statement

You are given the head of a singly linked list. Reorder it to:
`L0 → Ln → L1 → Ln-1 → L2 → Ln-2 → …`

You may not modify the values in the nodes. Only nodes themselves may be changed.

### Examples

**Example 1:**
```
Input: head = [1,2,3,4]
Output: [1,4,2,3]
```

**Example 2:**
```
Input: head = [1,2,3,4,5]
Output: [1,5,2,4,3]
```

---

## 🧠 Thought Process

### Three Steps:
1. **Find middle** - Using slow/fast pointers
2. **Reverse second half** - Standard reversal
3. **Merge alternately** - Interleave two halves

---

## 💡 Solution

```python
def reorderList(head: ListNode) -> None:
    if not head or not head.next:
        return
    
    # Step 1: Find middle
    slow, fast = head, head
    while fast.next and fast.next.next:
        slow = slow.next
        fast = fast.next.next
    
    # Step 2: Reverse second half
    prev, curr = None, slow.next
    slow.next = None  # Cut the list
    
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    
    # Step 3: Merge two halves
    first, second = head, prev
    while second:
        tmp1, tmp2 = first.next, second.next
        first.next = second
        second.next = tmp1
        first, second = tmp1, tmp2
```

---

## 🔍 Detailed Walkthrough

```
Input: 1 → 2 → 3 → 4 → 5

Step 1: Find middle
  slow at 3, fast at 5
  First half: 1 → 2 → 3
  Second half: 4 → 5

Step 2: Reverse second half
  4 → 5 becomes 5 → 4

Step 3: Merge
  1 → 5 → 2 → 4 → 3

Result: [1, 5, 2, 4, 3] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Three classic operations** - Find middle, reverse, merge
2. **Slow/fast pointers** - Find middle in O(n)
3. **In-place** - No extra space needed
4. **Common pattern** - Combine multiple LL techniques

---

## 🔗 Related Problems
- Palindrome Linked List
- Odd Even Linked List
- Split Linked List in Parts
