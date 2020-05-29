<https://leetcode.com/problems/course-schedule/>

We need to find out if there is a cycle in the directed graph, and the idea is [topological sorting](https://en.wikipedia.org/wiki/Topological_sorting).

One way to do this is using the idea of DFS: set the status of each vertex to `0` at the very beginning. Visit (DFS) all the vertices:

- If the status of the vertex is `1` (already visited), just skip it and continue
- If `-1` (temporarily visited), it indicates that there is a cycle in the graph, so set the result to `False`
- Otherwise, mark the vertex with `-1` status first, visit all the vertices connected from it, and set the status to `1` to show that the visit is finished.

```python
class Solution:
    
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
              
        self.adj_list = [[] for _ in range(numCourses)]
        self.status = [0] * numCourses
        self.res = True
        for u,v in prerequisites:
            self.adj_list[u].append(v)
        for i in range(numCourses):
            self.dfs(i)
        return self.res
    
    def dfs(self, u):
        if self.status[u] == 1:
            return
        if self.status[u] == -1:
            self.res = False
            return
        self.status[u] = -1
        for v in self.adj_list[u]:
            self.dfs(v)
        self.status[u] = 1
```

The other way is using BFS: use a queue to maintain the vertices with 0 in-degree, and for each of the vertex `u` in the queue, dequeue it and decrease the in-degree of all the vertices connected from `u` by 1. When the queue becomes empty, check if the in-degree of all the vertices are decreased to 0: if not, then there must be a cycle in the graph.

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        in_degree = [0] * numCourses
        adj_list = [[] for _ in range(numCourses)]
        for u,v in prerequisites:
            in_degree[v] += 1
            adj_list[u].append(v)
        queue = [i for i in range(numCourses) if in_degree[i] == 0]
        while queue:
            u = queue.pop(0)
            for v in adj_list[u]:
                in_degree[v] -= 1
                if in_degree[v] == 0:
                    queue.append(v)
        return not any(in_degree)
```

