# Design Twitter

## 📋 Problem Statement

Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and see the 10 most recent tweets in the user's news feed.

Implement the `Twitter` class:
- `Twitter()` Initializes your twitter object.
- `void postTweet(int userId, int tweetId)` Composes a new tweet with ID `tweetId` by the user `userId`.
- `List<Integer> getNewsFeed(int userId)` Retrieves the 10 most recent tweet IDs in the user's news feed (including their own tweets and tweets from people they follow).
- `void follow(int followerId, int followeeId)` The user with ID `followerId` follows the user with ID `followeeId`.
- `void unfollow(int followerId, int followeeId)` The user with ID `followerId` unfollows the user with ID `followeeId`.

---

## 💡 Solution

```python
import heapq
from collections import defaultdict

class Twitter:
    def __init__(self):
        self.tweets = defaultdict(list)  # userId -> [(time, tweetId)]
        self.following = defaultdict(set)  # userId -> set of followeeIds
        self.time = 0
    
    def postTweet(self, userId: int, tweetId: int) -> None:
        self.tweets[userId].append((self.time, tweetId))
        self.time += 1
    
    def getNewsFeed(self, userId: int) -> list[int]:
        # Get all users to check (self + following)
        users = self.following[userId] | {userId}
        
        # Merge k sorted lists using heap
        heap = []
        for user in users:
            if self.tweets[user]:
                idx = len(self.tweets[user]) - 1
                time, tweetId = self.tweets[user][idx]
                heap.append((-time, tweetId, user, idx))
        
        heapq.heapify(heap)
        
        result = []
        while heap and len(result) < 10:
            _, tweetId, user, idx = heapq.heappop(heap)
            result.append(tweetId)
            
            if idx > 0:
                time, tid = self.tweets[user][idx - 1]
                heapq.heappush(heap, (-time, tid, user, idx - 1))
        
        return result
    
    def follow(self, followerId: int, followeeId: int) -> None:
        self.following[followerId].add(followeeId)
    
    def unfollow(self, followerId: int, followeeId: int) -> None:
        self.following[followerId].discard(followeeId)
```

---

## 📊 Complexity Analysis

| Operation | Time | Space |
|-----------|------|-------|
| postTweet | O(1) | O(1) |
| getNewsFeed | O(k log k) | O(k) |
| follow | O(1) | O(1) |
| unfollow | O(1) | O(1) |

Where k = number of followees

---

## 🎯 Key Takeaways

1. **Merge k sorted lists** - For news feed
2. **Timestamp for ordering** - Global counter
3. **Include self in feed** - User sees own tweets
4. **Heap for top k** - Efficient retrieval

---

## 🔗 Related Problems
- Merge k Sorted Lists
- Top K Frequent Elements
