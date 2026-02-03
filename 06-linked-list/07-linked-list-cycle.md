# Linked List Cycle

## 📋 Problem Statement

Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle if some node can be reached again by continuously following the `next` pointer.

Return `true` if there is a cycle, otherwise `false`.

### Examples

**Example 1:**
```
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: Tail connects to index 1 (node with value 2)
```

**Example 2:**
```
Input: head = [1,2], pos = 0
Output: true
```

**Example 3:**
```
Input: head = [1], pos = -1
Output: false
```

### Constraints
- Number of nodes is in range `[0, 10^4]`
- `-10^5 <= Node.val <= 10^5`
- `pos` is `-1` or a valid index

---

## 🧠 Thought Process

### Step 1: Understand the Problem
- Detect if there's a cycle
- Can't just check for null (infinite loop if cycle!)

### Step 2: Key Insight 💡
**Floyd's Cycle Detection (Tortoise and Hare)**:
- Slow pointer moves 1 step
- Fast pointer moves 2 steps
- If cycle exists, they WILL meet!

**Why?** Fast gains 1 step per iteration. In a cycle, eventually catches slow.

---

## 💡 Solution

```python
def hasCycle(head: ListNode) -> bool:
    if not head or not head.next:
        return False
    
    slow = head
    fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    return False
```

---

## 🔍 Detailed Walkthrough

```
List: 3 → 2 → 0 → -4 → (back to 2)

Initial: slow=3, fast=3

Step 1: slow=2, fast=0
Step 2: slow=0, fast=2
Step 3: slow=-4, fast=-4 ← MEET!

Return True ✓
```

---

## 📊 Why They Meet (Math)

If cycle length = C, and slow enters cycle:
- Fast is some distance ahead
- Gap decreases by 1 each step
- They meet within C steps

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Floyd's Algorithm** - Two pointers, different speeds
2. **Fast checks both** - `fast and fast.next`
3. **Meet = cycle** - Can't meet otherwise
4. **O(1) space** - No extra data structures

---

## 🔗 Related Problems
- Linked List Cycle II (find cycle start)
- Find the Duplicate Number (same technique!)
- Happy Number
