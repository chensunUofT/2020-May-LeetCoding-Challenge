<https://leetcode.com/problems/uncrossed-lines/>

The algorithm is very similar with [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/): use a 2-D `dp` array to record the result for two subarrays `A[0] ... A[i]` and `B[0] ... B[j]`, and update `dp[i][j]` with previous states.

```python
class Solution:
    def maxUncrossedLines(self, A: List[int], B: List[int]) -> int:
        dp = [[0 for _ in range(len(B))] for _ in range(len(A))]
        for i in range(len(A)):
            for j in range(len(B)):
                if A[i] == B[j]:
                    dp[i][j] = 1 + (dp[i-1][j-1] if (i and j) else 0)
                else:
                    dp[i][j] = max((dp[i-1][j] if i else 0), (dp[i][j-1] if j else 0))
        return dp[-1][-1]                        
```



