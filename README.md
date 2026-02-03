# 🗺️ NeetCode 150 - Master Index

> Your complete lazy-friendly guide organized by topic

---

## 📚 Table of Contents

| # | Topic | Problems | Difficulty | File |
|---|-------|----------|------------|------|
| 1 | Arrays & Hashing | 9 | ⭐-⭐⭐ | [00-arrays-hashing.md](01-arrays-hashing/00-arrays-hashing.md) |
| 2 | Two Pointers | 5 | ⭐-⭐⭐⭐ | [00-two-pointers.md](02-two-pointers/00-two-pointers.md) |
| 3 | Sliding Window | 6 | ⭐-⭐⭐⭐ | [00-sliding-window.md](03-sliding-window/00-sliding-window.md) |
| 4 | Stack | 7 | ⭐-⭐⭐⭐ | [00-stack.md](04-stack/00-stack.md) |
| 5 | Binary Search | 7 | ⭐-⭐⭐⭐ | [00-binary-search.md](05-binary-search/00-binary-search.md) |
| 6 | Linked List | 11 | ⭐-⭐⭐⭐ | [00-linked-list.md](06-linked-list/00-linked-list.md) |
| 7 | Trees | 15 | ⭐-⭐⭐⭐ | [00-trees.md](07-trees/00-trees.md) |
| 8 | Tries | 3 | ⭐⭐-⭐⭐⭐ | [00-tries.md](08-tries/00-tries.md) |
| 9 | Heap / Priority Queue | 7 | ⭐-⭐⭐⭐ | [00-heap-priority-queue.md](09-heap-priority-queue/00-heap-priority-queue.md) |
| 10 | Backtracking | 9 | ⭐⭐-⭐⭐⭐ | [00-backtracking.md](10-backtracking/00-backtracking.md) |
| 11 | Graphs | 13 | ⭐⭐-⭐⭐⭐ | [00-graphs.md](11-graphs/00-graphs.md) |
| 12 | Advanced Graphs | 6 | ⭐⭐-⭐⭐⭐ | [00-advanced-graphs.md](12-advanced-graphs/00-advanced-graphs.md) |
| 13 | 1-D Dynamic Programming | 12 | ⭐-⭐⭐⭐ | [00-dynamic-programming-1d.md](13-dynamic-programming-1d/00-dynamic-programming-1d.md) |
| 14 | 2-D Dynamic Programming | 11 | ⭐⭐-⭐⭐⭐ | [00-dynamic-programming-2d.md](14-dynamic-programming-2d/00-dynamic-programming-2d.md) |
| 15 | Greedy | 8 | ⭐⭐-⭐⭐ | [00-greedy.md](15-greedy/00-greedy.md) |
| 16 | Intervals | 6 | ⭐-⭐⭐⭐ | [00-intervals.md](16-intervals/00-intervals.md) |
| 17 | Math & Geometry | 8 | ⭐-⭐⭐ | [00-math-geometry.md](17-math-geometry/00-math-geometry.md) |
| 18 | Bit Manipulation | 7 | ⭐-⭐⭐ | [00-bit-manipulation.md](18-bit-manipulation/00-bit-manipulation.md) |

**Total: 150 Problems** ✅

---

## 🎯 Quick Pattern Reference

### Data Structures
- **HashMap/HashSet** → Duplicates, frequencies, O(1) lookup
- **Stack** → Matching pairs, monotonic problems, LIFO
- **Queue** → BFS, level order, FIFO
- **Heap** → Kth largest/smallest, merge k lists
- **Trie** → Prefix operations, word search

### Algorithms
- **Two Pointers** → Sorted arrays, pairs/triplets
- **Sliding Window** → Subarray/substring problems
- **Binary Search** → Sorted space, "find min/max satisfying"
- **DFS** → Explore all paths, backtracking
- **BFS** → Shortest path, level-by-level
- **DP** → Optimal substructure, overlapping subproblems
- **Greedy** → Local optimum → global optimum

---

## 📊 Difficulty Distribution

| Easy | Medium | Hard |
|------|--------|------|
| ~20 | ~100 | ~30 |

---

## 💡 How to Use This Guide

### 🏃 Quick Revision Mode (Lazy!)
1. Open relevant topic file
2. Read only **"The Trick"** section for each problem
3. Glance at **"Remember"** line
4. Move to next problem
5. **Time:** ~2-3 minutes per topic

### 📖 Deep Study Mode
1. Read full problem summary
2. Understand the pattern
3. Check the template/code snippet
4. Review common mistakes
5. **Time:** ~10-15 minutes per topic

### 🎯 Practice Mode
1. Read "The Trick"
2. Try to code it yourself
3. Come back if stuck
4. Review the pattern section
5. **Time:** ~30+ minutes per topic

---

## 🗂️ Study Order Recommendations

### For Beginners:
1. Arrays & Hashing
2. Two Pointers
3. Stack
4. Sliding Window
5. Binary Search
6. Linked List
7. Trees
8. Graphs
9. 1-D DP
10. (Continue with rest)

### For Interview Prep (Most Common):
1. Arrays & Hashing ⭐⭐⭐⭐⭐
2. Two Pointers ⭐⭐⭐⭐⭐
3. Trees ⭐⭐⭐⭐⭐
4. Graphs ⭐⭐⭐⭐
5. 1-D DP ⭐⭐⭐⭐
6. Sliding Window ⭐⭐⭐⭐
7. Intervals ⭐⭐⭐
8. Binary Search ⭐⭐⭐
9. Stack ⭐⭐⭐
10. (Rest as needed)

### For FAANG:
**All topics equally important!** Focus on:
- Hard problems in each category
- Time/space optimization
- Edge cases
- Multiple approaches

---

## 🧠 Memory Aids

### Quick Pattern Matching
- **Substring/Subarray** → Sliding Window
- **Sorted Array** → Two Pointers or Binary Search
- **Find pairs/triplets** → Two Pointers or HashMap
- **Parentheses/Nesting** → Stack
- **All combinations** → Backtracking
- **Optimal solution** → DP or Greedy
- **Graph traversal** → BFS/DFS
- **Shortest path** → BFS (unweighted) or Dijkstra
- **Kth largest/smallest** → Heap

### When Stuck
1. Can I sort it? → Try two pointers
2. Need all solutions? → Backtracking
3. Need optimal solution? → Try DP, then Greedy
4. Is it a graph? → Think BFS/DFS
5. Involves ranges/intervals? → Sort first
6. Need fast lookup? → HashMap/HashSet

---

## 📈 Progress Tracking

Create your own checklist:
```
[ ] 01. Arrays & Hashing (9/9)
[ ] 02. Two Pointers (5/5)
[ ] 03. Sliding Window (6/6)
...
```

---

## 🎓 Pro Tips

✅ **For Revision:**
- Read "The Trick" section only
- Practice writing the key line from memory
- Can you explain it in 30 seconds?

✅ **For Understanding:**
- Draw examples on paper
- Code without looking at solution
- Explain to rubber duck 🦆

✅ **For Interviews:**
- State the approach first
- Mention time/space complexity
- Start with brute force, optimize
- Talk through your thought process

---

## 🔥 Super Lazy Mode

Just read these:
1. The file's **Pattern Recognition** section
2. **"The Trick"** for each problem
3. **Key Insights** at the end

**Time:** 5 minutes per topic, ~90 minutes total!

---

## 📝 Notes Section

Use this space to track:
- Problems you found tricky
- Topics needing more review
- Personal insights
- Interview experiences

---

**Good luck! You got this! 🚀**

*Remember: Consistency > Intensity. Better to do 5 problems well than 20 problems poorly.*
