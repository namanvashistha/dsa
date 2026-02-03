# K Closest Points to Origin

## 📋 Problem Statement

Given an array of `points` where `points[i] = [xi, yi]` represents a point on the X-Y plane and an integer `k`, return the `k` closest points to the origin `(0, 0)`.

### Examples

**Example 1:**
```
Input: points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]
Explanation: Distance of (1,3) = sqrt(10), (-2,2) = sqrt(8)
```

---

## 💡 Solution: Max Heap

```python
import heapq

def kClosest(points: list[list[int]], k: int) -> list[list[int]]:
    # Max heap of size k (negate distance)
    heap = []
    
    for x, y in points:
        dist = x*x + y*y  # No need for sqrt
        
        if len(heap) < k:
            heapq.heappush(heap, (-dist, x, y))
        elif -dist > heap[0][0]:
            heapq.heapreplace(heap, (-dist, x, y))
    
    return [[x, y] for _, x, y in heap]
```

## 💡 Solution: QuickSelect

```python
def kClosest(points: list[list[int]], k: int) -> list[list[int]]:
    def dist(point):
        return point[0]**2 + point[1]**2
    
    def partition(l, r):
        pivot = dist(points[r])
        i = l
        for j in range(l, r):
            if dist(points[j]) <= pivot:
                points[i], points[j] = points[j], points[i]
                i += 1
        points[i], points[r] = points[r], points[i]
        return i
    
    l, r = 0, len(points) - 1
    while l <= r:
        p = partition(l, r)
        if p == k:
            break
        elif p < k:
            l = p + 1
        else:
            r = p - 1
    
    return points[:k]
```

---

## 📊 Complexity Analysis

| Approach | Time | Space |
|----------|------|-------|
| Max Heap | O(n log k) | O(k) |
| QuickSelect | O(n) avg | O(1) |

---

## 🎯 Key Takeaways

1. **Skip sqrt** - Compare squared distances
2. **Max heap of k** - Keep k smallest
3. **QuickSelect** - O(n) average alternative

---

## 🔗 Related Problems
- Kth Largest Element
- Top K Frequent Elements
