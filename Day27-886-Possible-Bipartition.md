<https://leetcode.com/problems/possible-bipartition/>

We can consider this as a graph problem: coloring all the vertices in a non-directed graph with two colors (represented by `1` and `-1` in this solution), and checking if there're connected vertices with same color. Firstly, construct a `table` where `table[i]` contains all the vertices connected with vertex `i`. Then, start traversing the graph with a DFS pattern and coloring each uncolored vertex with a different color from the previous level of the DFS. If we have two connected vertices with same color, then the bipartition is not possible.

```python
class Solution:
    def possibleBipartition(self, N: int, dislikes: List[List[int]]) -> bool:
        
        def dfs(i, c):
            color[i] = c
            for j in table[i]:
                if color[j] == c:
                    return False
                if (not color[j]) and (not dfs(j, -c)):
                    return False
            return True
        
        table = [[] for _ in range(N+1)]
        for a,b in dislikes:
            table[a].append(b)
            table[b].append(a)
        color = [0 for _ in range(N+1)]
        for i in range(1, N+1):
            if (not color[i]) and (not dfs(i, 1)):
                return False
        return True
```



