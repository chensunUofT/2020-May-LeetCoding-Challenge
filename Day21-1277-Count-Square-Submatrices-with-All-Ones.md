<https://leetcode.com/problems/count-square-submatrices-with-all-ones/>

The Dynamic Programming idea is the same as in [Maximal Square](https://leetcode.com/problems/maximal-square/): the number of squares (or the side length of the big square, **they are equivalent**) with bottom-right corner at position `(i, j)` depends on **its top, left and left-top**. If the value itself is `0`, then the number of squares must be `0` as well, and that point does not contribute to the result; if the value is `1`, then it should be updated with one plus the minimum value of the three.

```python
class Solution:
    def countSquares(self, matrix: List[List[int]]) -> int:    
        m, n = len(matrix), len(matrix[0])
        res = 0
        for i in range(m):
            for j in range(n):
                if matrix[i][j]:
                    if i and j:
                        matrix[i][j] = 1 + min(matrix[i-1][j], matrix[i][j-1], matrix[i-1][j-1])
                        res += matrix[i][j]
                    else:
                        res += 1
        return res
```

