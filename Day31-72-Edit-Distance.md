<https://leetcode.com/problems/edit-distance/>

A typical DP problem: we use `dp[i][j]` to represent the edit distance between `word1[0...i]` (the first `i` letters) and `word2[0...j]`. When calculating `dp[i][j]`, if `word1[i-1] == word2[j-1]` which means that the two substrings end with the same letter, it just equals to `dp[i-1][j-1]`; otherwise, considering that `word1[0...i]` could come from replacing, inserting or deleting a character, `dp[i][j]` should be one plus **the minimum among `dp[i-1][j-1]`, `dp[i][j-1]` and `dp[i-1][j]`**.

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        if not m or not n:
            return m+n
        dp = [[_ for _ in range(n + 1)] for _ in range(m + 1)]
        for i in range(m + 1):
            for j in range(n + 1):
                if not i or not j:
                    dp[i][j] = i + j
                else:
                    if word1[i-1] == word2[j-1]:
                        dp[i][j] = dp[i-1][j-1]
                    else:
                        dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1
        return dp[-1][-1]
```

