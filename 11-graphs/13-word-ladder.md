# Word Ladder

## 📋 Problem Statement

A transformation sequence from word `beginWord` to `endWord` using a dictionary `wordList` is a sequence such that:
- The first word is `beginWord`
- The last word is `endWord`
- Only one letter can be changed at a time
- Every word in the sequence is in `wordList`

Return the number of words in the shortest transformation sequence, or `0` if no such sequence exists.

### Examples

**Example 1:**
```
Input: beginWord = "hit", endWord = "cog", 
       wordList = ["hot","dot","dog","lot","log","cog"]
Output: 5
Explanation: hit → hot → dot → dog → cog
```

---

## 🧠 Thought Process

### Key Insight 💡
**BFS for shortest path!**
- Each word = node
- Edge = one letter difference
- Find shortest path from begin to end

---

## 💡 Solution

```python
from collections import deque

def ladderLength(beginWord: str, endWord: str, wordList: list[str]) -> int:
    word_set = set(wordList)
    if endWord not in word_set:
        return 0
    
    queue = deque([(beginWord, 1)])
    visited = {beginWord}
    
    while queue:
        word, length = queue.popleft()
        
        if word == endWord:
            return length
        
        # Try changing each character
        for i in range(len(word)):
            for c in 'abcdefghijklmnopqrstuvwxyz':
                new_word = word[:i] + c + word[i+1:]
                
                if new_word in word_set and new_word not in visited:
                    visited.add(new_word)
                    queue.append((new_word, length + 1))
    
    return 0
```

---

## 📊 Complexity Analysis

| Metric | Value |
|--------|-------|
| Time | O(M² × N) |
| Space | O(M × N) |

Where M = word length, N = number of words

---

## 🎯 Key Takeaways

1. **BFS for shortest path** - Unweighted graph
2. **Generate neighbors** - Change each char to a-z
3. **Use set for O(1) lookup** - Check if word exists
4. **Track visited** - Avoid revisiting

---

## 🔗 Related Problems
- Word Ladder II (return all paths)
- Minimum Genetic Mutation
