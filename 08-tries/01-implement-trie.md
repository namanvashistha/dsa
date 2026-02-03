# Implement Trie (Prefix Tree)

## 📋 Problem Statement

A **trie** (pronounced as "try") or **prefix tree** is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. 

Implement the Trie class:
- `Trie()` Initializes the trie object.
- `void insert(String word)` Inserts the string `word` into the trie.
- `boolean search(String word)` Returns `true` if `word` is in the trie.
- `boolean startsWith(String prefix)` Returns `true` if there is a previously inserted string that has the prefix `prefix`.

### Examples

```
Input: ["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
       [[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
Output: [null, null, true, false, true, null, true]
```

---

## 🧠 Thought Process

### Step 1: Understand Trie Structure
- Each node represents a character
- Nodes have children (up to 26 for lowercase)
- Special flag for "end of word"

### Step 2: Visual Structure
```
Insert "apple", "app":

        root
          |
          a
          |
          p
          |
          p (end of word for "app")
          |
          l
          |
          e (end of word for "apple")
```

---

## 💡 Solution

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.is_end = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end = True
    
    def search(self, word: str) -> bool:
        node = self._find_node(word)
        return node is not None and node.is_end
    
    def startsWith(self, prefix: str) -> bool:
        return self._find_node(prefix) is not None
    
    def _find_node(self, s: str) -> TrieNode:
        node = self.root
        for char in s:
            if char not in node.children:
                return None
            node = node.children[char]
        return node
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| Insert | O(m) | O(m) |
| Search | O(m) | O(1) |
| StartsWith | O(m) | O(1) |

Where m = length of word/prefix

---

## 🎯 Key Takeaways

1. **Trie = prefix tree** - Efficient for prefix operations
2. **is_end flag** - Distinguishes complete words
3. **HashMap for children** - Or array of 26 for lowercase
4. **Shared prefixes** - Space efficient for similar words

---

## 🔗 Related Problems
- Word Search II (Trie + DFS)
- Design Add and Search Words
- Implement Magic Dictionary
