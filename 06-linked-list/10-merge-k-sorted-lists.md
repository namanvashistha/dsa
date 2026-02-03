# Merge K Sorted Lists

## 📋 Problem Statement

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

### Examples

**Example 1:**
```
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
```

---

## 🧠 Thought Process

### Approaches:
1. **Brute Force:** Merge one by one - O(kN)
2. **Min Heap:** Always pick smallest - O(N log k)
3. **Divide & Conquer:** Merge pairs - O(N log k)

---

## 💡 Solution: Min Heap

```python
import heapq

def mergeKLists(lists: list[ListNode]) -> ListNode:
    dummy = ListNode(0)
    curr = dummy
    heap = []
    
    # Add first node from each list
    for i, lst in enumerate(lists):
        if lst:
            heapq.heappush(heap, (lst.val, i, lst))
    
    while heap:
        val, i, node = heapq.heappop(heap)
        curr.next = node
        curr = curr.next
        
        if node.next:
            heapq.heappush(heap, (node.next.val, i, node.next))
    
    return dummy.next
```

## 💡 Solution: Divide & Conquer

```python
def mergeKLists(lists: list[ListNode]) -> ListNode:
    if not lists:
        return None
    
    def mergeTwoLists(l1, l2):
        dummy = ListNode(0)
        curr = dummy
        while l1 and l2:
            if l1.val <= l2.val:
                curr.next = l1
                l1 = l1.next
            else:
                curr.next = l2
                l2 = l2.next
            curr = curr.next
        curr.next = l1 or l2
        return dummy.next
    
    while len(lists) > 1:
        merged = []
        for i in range(0, len(lists), 2):
            l1 = lists[i]
            l2 = lists[i + 1] if i + 1 < len(lists) else None
            merged.append(mergeTwoLists(l1, l2))
        lists = merged
    
    return lists[0]
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Min Heap | O(N log k) | O(k) |
| Divide & Conquer | O(N log k) | O(log k) |

Where N = total nodes, k = number of lists

---

## 🎯 Key Takeaways

1. **Min heap for k-way merge** - O(log k) per node
2. **Divide & conquer** - Merge pairs like merge sort
3. **Use index for tie-breaking** - In heap comparison
4. **Both approaches O(N log k)** - Choose based on preference

---

## 🔗 Related Problems
- Merge Two Sorted Lists
- Ugly Number II
- Smallest Range Covering Elements from K Lists
