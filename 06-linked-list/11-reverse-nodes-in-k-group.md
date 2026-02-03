# Reverse Nodes in k-Group

## 📋 Problem Statement

Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return the modified list.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes at the end should remain as is.

### Examples

**Example 1:**
```
Input: head = [1,2,3,4,5], k = 2
Output: [2,1,4,3,5]
```

**Example 2:**
```
Input: head = [1,2,3,4,5], k = 3
Output: [3,2,1,4,5]
```

---

## 🧠 Thought Process

### Key Steps:
1. Check if k nodes exist
2. Reverse k nodes
3. Connect reversed group to next group
4. Recurse/iterate for remaining

---

## 💡 Solution

```python
def reverseKGroup(head: ListNode, k: int) -> ListNode:
    # Check if k nodes exist
    count = 0
    curr = head
    while curr and count < k:
        curr = curr.next
        count += 1
    
    if count < k:
        return head  # Not enough nodes
    
    # Reverse k nodes
    prev, curr = None, head
    for _ in range(k):
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    
    # head is now tail of reversed group
    # Connect to next group
    head.next = reverseKGroup(curr, k)
    
    return prev  # prev is new head
```

---

## 🔍 Detailed Walkthrough

```
head = [1,2,3,4,5], k = 2

First group: Reverse 1,2
  Before: 1 → 2 → 3 → 4 → 5
  After:  2 → 1    3 → 4 → 5
  
Second group: Reverse 3,4
  Before: 3 → 4 → 5
  After:  4 → 3    5
  
Third group: Only 5, keep as is

Connect:
  2 → 1 → 4 → 3 → 5

Result: [2,1,4,3,5] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(n/k) recursion stack |

---

## 🎯 Key Takeaways

1. **Count first** - Ensure k nodes exist
2. **Standard reversal** - For k nodes
3. **Connect tail** - Old head becomes tail, link to next group
4. **Recursion** - Clean solution (can also iterate)

---

## 🔗 Related Problems
- Reverse Linked List
- Swap Nodes in Pairs
- Reverse Linked List II
