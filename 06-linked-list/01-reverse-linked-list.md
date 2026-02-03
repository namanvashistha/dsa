# Reverse Linked List

## 📋 Problem Statement

Given the `head` of a singly linked list, reverse the list, and return the reversed list.

### Examples

**Example 1:**
```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

**Example 2:**
```
Input: head = [1,2]
Output: [2,1]
```

**Example 3:**
```
Input: head = []
Output: []
```

### Constraints
- The number of nodes is in the range `[0, 5000]`
- `-5000 <= Node.val <= 5000`

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Reverse all pointers
- 1→2→3 becomes 3→2→1
- Return new head (was tail)

### Step 2: Key Insight 💡
Use **three pointers**: prev, curr, next
1. Save next node
2. Point current to previous
3. Move prev and curr forward

---

## 💡 Solution Approaches

### Approach 1: Iterative (Three Pointers)

```python
def reverseList(head: ListNode) -> ListNode:
    prev = None
    curr = head
    
    while curr:
        next_node = curr.next  # Save next
        curr.next = prev       # Reverse pointer
        prev = curr            # Move prev forward
        curr = next_node       # Move curr forward
    
    return prev
```

### Approach 2: Recursive

```python
def reverseList(head: ListNode) -> ListNode:
    if not head or not head.next:
        return head
    
    new_head = reverseList(head.next)
    head.next.next = head
    head.next = None
    
    return new_head
```

---

## 🔍 Detailed Walkthrough (Iterative)

```
Initial: 1 → 2 → 3 → None
         prev=None, curr=1

Step 1:
  next_node = 2
  1.next = None (was 2)
  prev = 1, curr = 2
  
  None ← 1    2 → 3 → None

Step 2:
  next_node = 3
  2.next = 1 (was 3)
  prev = 2, curr = 3
  
  None ← 1 ← 2    3 → None

Step 3:
  next_node = None
  3.next = 2 (was None)
  prev = 3, curr = None
  
  None ← 1 ← 2 ← 3

curr is None → return prev (3)
Result: 3 → 2 → 1 → None ✓
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Iterative | O(n) | O(1) |
| Recursive | O(n) | O(n) |

---

## 🎯 Key Takeaways

1. **Three pointers pattern** - prev, curr, next
2. **Save next before modifying** - Don't lose reference!
3. **prev starts as None** - New tail points to None
4. **Return prev** - New head (was tail)

---

## 🔗 Related Problems
- Reverse Linked List II (reverse portion)
- Palindrome Linked List
- Reverse Nodes in k-Group
