# Add Two Numbers

## 📋 Problem Statement

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each node contains a single digit.

Add the two numbers and return the sum as a linked list.

### Examples

**Example 1:**
```
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807
```

---

## 🧠 Thought Process

### Key Insight 💡
- Reversed order = units digit first (perfect for addition!)
- Process digit by digit
- Track carry

---

## 💡 Solution

```python
def addTwoNumbers(l1: ListNode, l2: ListNode) -> ListNode:
    dummy = ListNode(0)
    curr = dummy
    carry = 0
    
    while l1 or l2 or carry:
        val1 = l1.val if l1 else 0
        val2 = l2.val if l2 else 0
        
        total = val1 + val2 + carry
        carry = total // 10
        curr.next = ListNode(total % 10)
        curr = curr.next
        
        l1 = l1.next if l1 else None
        l2 = l2.next if l2 else None
    
    return dummy.next
```

---

## 🔍 Detailed Walkthrough

```
l1: 2 → 4 → 3 (342)
l2: 5 → 6 → 4 (465)

Step 1: 2 + 5 + 0 = 7, carry=0 → Node(7)
Step 2: 4 + 6 + 0 = 10, carry=1 → Node(0)
Step 3: 3 + 4 + 1 = 8, carry=0 → Node(8)

Result: 7 → 0 → 8 (807) ✓
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(max(m, n)) |
| Space | O(max(m, n)) |

---

## 🎯 Key Takeaways

1. **Reversed = easy addition** - Start from units
2. **Handle different lengths** - Use 0 for missing digits
3. **Don't forget final carry** - Check `or carry`
4. **Dummy head** - Simplifies list construction

---

## 🔗 Related Problems
- Add Two Numbers II (not reversed)
- Multiply Strings
- Plus One Linked List
