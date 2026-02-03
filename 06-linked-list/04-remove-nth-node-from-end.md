# Remove Nth Node From End of List

## 📋 Problem Statement

Given the `head` of a linked list, remove the `n`th node from the end of the list and return its head.

### Examples

**Example 1:**
```
Input: head = [1,2,3,4,5], n = 2
Output: [1,2,3,5]
```

**Example 2:**
```
Input: head = [1], n = 1
Output: []
```

---

## 🧠 Thought Process

### Key Insight 💡
Use **two pointers** with n-node gap:
1. Move fast n steps ahead
2. Move both until fast reaches end
3. Slow is at node before target

---

## 💡 Solution

```python
def removeNthFromEnd(head: ListNode, n: int) -> ListNode:
    dummy = ListNode(0, head)
    slow = fast = dummy
    
    # Move fast n+1 steps ahead
    for _ in range(n + 1):
        fast = fast.next
    
    # Move both until fast reaches end
    while fast:
        slow = slow.next
        fast = fast.next
    
    # Remove the nth node
    slow.next = slow.next.next
    
    return dummy.next
```

---

## 🔍 Detailed Walkthrough

```
head = [1, 2, 3, 4, 5], n = 2

dummy → 1 → 2 → 3 → 4 → 5 → None

Move fast 3 steps (n+1):
fast at 3

Move both:
slow at 1, fast at 4
slow at 2, fast at 5
slow at 3, fast at None

slow.next = slow.next.next
3 → 5 (skipping 4)

Result: [1, 2, 3, 5] ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

**One pass solution!**

---

## 🎯 Key Takeaways

1. **Two pointers with gap** - Classic pattern
2. **Dummy node** - Handles removing head
3. **n+1 gap** - To land at node BEFORE target
4. **Single pass** - Efficient

---

## 🔗 Related Problems
- Delete Node in a Linked List
- Swapping Nodes in a Linked List
- Delete the Middle Node
