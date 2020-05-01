<https://leetcode.com/problems/first-bad-version/>

Use a binary search to narrow down the range where the "First bad version" is located:

- If `isBadVersion(mid)` is `True`, then the "First bad version" has to be itself or on its left;
- If `isBadVersion(mid)` is `False`, then the "First bad version" has to be on its right.

When the range is narrowed down to contain only one element, it is the value that we're looking for.

```python
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return a bool
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        low, high = 1, n
        while low < high:
            mid = (low + high) // 2
            if isBadVersion(mid):
                high = mid
            else:
                low = mid + 1
        return low
        
```

