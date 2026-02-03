# Merge Two Sorted Lists

## 📋 Problem Statement

You are given the heads of two sorted linked lists `list1` and `list2`.

Merge the two lists into one **sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

### Examples

**Example 1:**
```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```

---

## 🧠 Thought Process

### Key Insight 💡
Use **dummy node** and compare nodes one by one.

1. Create dummy head
2. Compare current nodes, attach smaller
3. Move pointer forward
4. Attach remaining nodes

---

## 💡 Solution

```python
def mergeTwoLists(list1: ListNode, list2: ListNode) -> ListNode:
    dummy = ListNode(0)
    curr = dummy
    
    while list1 and list2:
        if list1.val <= list2.val:
            curr.next = list1
            list1 = list1.next
        else:
            curr.next = list2
            list2 = list2.next
        curr = curr.next
    
    # Attach remaining
    curr.next = list1 if list1 else list2
    
    return dummy.next
```

---

## 🔍 Detailed Walkthrough

```
list1: 1 → 2 → 4
list2: 1 → 3 → 4

dummy → 

Compare 1 vs 1: attach list1's 1
dummy → 1
list1: 2 → 4

Compare 2 vs 1: attach list2's 1
dummy → 1 → 1
list2: 3 → 4

Compare 2 vs 3: attach list1's 2
dummy → 1 → 1 → 2
list1: 4

Compare 4 vs 3: attach list2's 3
dummy → 1 → 1 → 2 → 3
list2: 4

Compare 4 vs 4: attach list1's 4
dummy → 1 → 1 → 2 → 3 → 4
list1: null

Attach remaining list2
dummy → 1 → 1 → 2 → 3 → 4 → 4

Result: 1 → 1 → 2 → 3 → 4 → 4 ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(n + m) |
| Space | O(1) |

---

## 🎯 Key Takeaways

1. **Dummy node pattern** - Simplifies edge cases
2. **Compare and attach** - Classic merge technique
3. **Handle remaining** - One list may be longer
4. **Return dummy.next** - Skip dummy

---

## 🔗 Related Problems
- Merge k Sorted Lists
- Sort List
- Merge Sorted Array
