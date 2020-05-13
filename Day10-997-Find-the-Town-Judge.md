<https://leetcode.com/problems/find-the-town-judge/>

Use two arrays to record the in-degrees and out-degrees of each node in the graph, and find out the node with `0` out-degree and `N-1` in-degree if it exists. 

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

Actually, using the difference between out-degree and in-degree could save half of the space, and there cannot be more than one *town judge* if you think about the math.

```python
class Solution:
    def findJudge(self, N: int, trust: List[List[int]]) -> int:
        degree = [0] * N
        for a,b in trust:
            degree[a-1] -= 1
            degree[b-1] += 1
        for i in range(N):
            if degree[i] == N-1:
                return i+1
        return -1
```

