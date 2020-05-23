<https://leetcode.com/problems/interval-list-intersections/>

Use two pointers `a` and `b` to refer to the intervals in the each of the lists. In each iteration, check if `a` and `b` overlap: if yes, then add the intersection to the result; move one of the pointers (**the one with the smaller ending point**) to the next interval in the list until out of index (there's no more interval in that list). 

```python
class Solution:
    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:
        i, j = 0, 0
        res = []
        while i < len(A) and j < len(B):
            a, b = A[i], B[j]
            if a[0] <= b[1] and b[0] <= a[1]:
                res.append([max(a[0], b[0]), min(a[1], b[1])])
            if a[1] < b[1]:
                i += 1
            else:
                j += 1
        return res
```

