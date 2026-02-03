# Time Based Key-Value Store

## 📋 Problem Statement

Design a time-based key-value data structure that can store multiple values for the same key at different timestamps and retrieve the key's value at a certain timestamp.

Implement the `TimeMap` class:
- `TimeMap()` Initializes the object.
- `void set(String key, String value, int timestamp)` Stores the key `key` with the value `value` at the given time `timestamp`.
- `String get(String key, int timestamp)` Returns a value such that `set` was called previously, with `timestamp_prev <= timestamp`. If there are multiple such values, it returns the value associated with the largest `timestamp_prev`. If there are no values, it returns `""`.

---

## 🧠 Thought Process

### Key Insight 💡
- Store (timestamp, value) pairs for each key
- Timestamps come in increasing order → already sorted!
- Binary search to find largest timestamp ≤ query

---

## 💡 Solution

```python
from collections import defaultdict
import bisect

class TimeMap:
    def __init__(self):
        self.store = defaultdict(list)  # key -> [(timestamp, value)]
    
    def set(self, key: str, value: str, timestamp: int) -> None:
        self.store[key].append((timestamp, value))
    
    def get(self, key: str, timestamp: int) -> str:
        if key not in self.store:
            return ""
        
        values = self.store[key]
        
        # Binary search for rightmost timestamp <= target
        left, right = 0, len(values) - 1
        result = ""
        
        while left <= right:
            mid = (left + right) // 2
            if values[mid][0] <= timestamp:
                result = values[mid][1]
                left = mid + 1
            else:
                right = mid - 1
        
        return result
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| set | O(1) | O(n) |
| get | O(log n) | O(1) |

---

## 🎯 Key Takeaways

1. **Timestamps sorted** - Given in increasing order
2. **Binary search** - Find floor timestamp
3. **Store pairs** - (timestamp, value)
4. **bisect module** - Alternative approach

---

## 🔗 Related Problems
- Snapshot Array
- Stock Price Fluctuation
