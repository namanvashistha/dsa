# 🌿 Tries (Prefix Trees) - NeetCode 150

> 3 problems | Master prefix storage and word search

---

## 1️⃣ Implement Trie ⭐⭐ Medium
**The Trick:** Tree where each node = character
- Each node has 26 children (a-z)
- Flag for end of word
- Insert: create path if not exists
- Search: follow path, check end flag
- **Remember:** Node = {children: {}, isEndOfWord: bool}

**Structure:**
```
     root
    /  |  \
   a   b   c
  /    |    \
 p     a     a
 |     |     |
 p     t     t
```

---

## 2️⃣ Design Add and Search Words Data Structure ⭐⭐ Medium
**The Trick:** Trie + DFS for wildcards
- Regular char: follow that child
- '.' wildcard: try all children (DFS/backtrack)
- Use recursion for '.' handling
- **Remember:** Wildcard = try all 26 children

**Key:**
- "bad" → normal trie
- "b.d" → try all children at position 1
- DFS explores all possibilities

---

## 3️⃣ Word Search II ⭐⭐⭐ Hard
**The Trick:** Trie + DFS on board
- Build trie with all words
- DFS on board, traverse trie simultaneously
- When reach end of word in trie → found word
- Mark visited cells, backtrack
- **Remember:** Trie guides the search

**Optimization:**
- Remove found words from trie (prune)
- Early termination when no children
- Mark cells to avoid revisiting

---

## 🎯 Pattern Recognition

**Use Trie when:**
- Prefix-based operations
- Multiple words to search
- Autocomplete functionality
- Word validation with prefixes
- Reducing repeated prefix storage

**Trie vs HashMap:**
- **Trie:** Better for prefix queries, space efficient for shared prefixes
- **HashMap:** Better for exact matches only

**Trie Node Structure:**
```python
class TrieNode:
    def __init__(self):
        self.children = {}  # or [None] * 26
        self.is_end_of_word = False
        # Optional: store word here for easy retrieval
```

**Common Operations:**

1. **Insert:** O(L) where L = word length
```python
node = root
for char in word:
    if char not in node.children:
        node.children[char] = TrieNode()
    node = node.children[char]
node.is_end_of_word = True
```

2. **Search:** O(L)
```python
node = root
for char in word:
    if char not in node.children:
        return False
    node = node.children[char]
return node.is_end_of_word
```

3. **StartsWith (Prefix):** O(L)
```python
node = root
for char in prefix:
    if char not in node.children:
        return False
    node = node.children[char]
return True  # Don't need is_end_of_word check
```

**Time Complexity:**
- Insert: O(L)
- Search: O(L)
- Space: O(ALPHABET_SIZE * L * N) worst case

**Common Mistakes:**
- Forgetting `is_end_of_word` flag
- Not backtracking in DFS problems
- Not pruning trie after finding words
- Using array[26] when characters not just a-z

**Key Insights:**
- Trie = efficient prefix storage
- Shared prefixes = shared nodes
- Wildcard search = DFS through trie
- Board + Trie = DFS on board guided by trie

**When NOT to use Trie:**
- Only checking if exact word exists → use HashSet
- Only a few words → HashMap is simpler
- No prefix operations needed
