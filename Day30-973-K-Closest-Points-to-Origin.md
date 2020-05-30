<https://leetcode.com/problems/k-closest-points-to-origin/>

Maintain a heap (priority queue) that stores point with smallest distance at the top, and return the top K elements. https://docs.python.org/3/library/heapq.html#heapq.nsmallest

```python
from collections import deque

class Solution:
    def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        return heapq.nsmallest(K, points, key=lambda p: p[0]**2 + p[1]**2)
```

