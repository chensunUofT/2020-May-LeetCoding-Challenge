<https://leetcode.com/problems/find-the-town-judge/>

```python
class Solution:
    def findJudge(self, N: int, trust: List[List[int]]) -> int:
        trust_out = [0] * N
        trust_in = [0] * N
        for t in trust:
            trust_out[t[0]-1] += 1
            trust_in[t[1]-1] += 1
        zipped = list(zip(trust_out, trust_in))
        return zipped.index((0, N-1)) + 1 if (0, N-1) in zipped else -1
```

