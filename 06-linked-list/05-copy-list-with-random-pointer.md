# Copy List with Random Pointer

## 📋 Problem Statement

A linked list of length `n` is given such that each node contains an additional random pointer, which could point to any node in the list, or `null`.

Construct a **deep copy** of the list.

### Examples

```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```

---

## 🧠 Thought Process

### Approach 1: HashMap
Map original nodes to cloned nodes, then set pointers.

### Approach 2: Interweaving (O(1) space)
1. Insert clones between originals: A → A' → B → B'
2. Set random pointers using this structure
3. Separate the two lists

---

## 💡 Solution: HashMap

```python
def copyRandomList(head: Node) -> Node:
    if not head:
        return None
    
    old_to_new = {}
    
    # First pass: create all nodes
    curr = head
    while curr:
        old_to_new[curr] = Node(curr.val)
        curr = curr.next
    
    # Second pass: set next and random pointers
    curr = head
    while curr:
        clone = old_to_new[curr]
        clone.next = old_to_new.get(curr.next)
        clone.random = old_to_new.get(curr.random)
        curr = curr.next
    
    return old_to_new[head]
```

---

## 💡 Solution: O(1) Space

```python
def copyRandomList(head: Node) -> Node:
    if not head:
        return None
    
    # Step 1: Interweave clones
    curr = head
    while curr:
        clone = Node(curr.val, curr.next)
        curr.next = clone
        curr = clone.next
    
    # Step 2: Set random pointers
    curr = head
    while curr:
        if curr.random:
            curr.next.random = curr.random.next
        curr = curr.next.next
    
    # Step 3: Separate lists
    curr = head
    clone_head = head.next
    while curr:
        clone = curr.next
        curr.next = clone.next
        clone.next = clone.next.next if clone.next else None
        curr = curr.next
    
    return clone_head
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| HashMap | O(n) | O(n) |
| Interweave | O(n) | O(1) |

---

## 🎯 Key Takeaways

1. **HashMap for mapping** - Original → Clone
2. **Two passes** - Create nodes, then set pointers
3. **Interweaving trick** - O(1) space alternative
4. **Random pointer challenge** - Can't just copy directly

---

## 🔗 Related Problems
- Clone Graph
- Clone Binary Tree With Random Pointer
