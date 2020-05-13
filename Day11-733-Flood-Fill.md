<https://leetcode.com/problems/flood-fill/>

```python
class Solution:
    
    def floodFill(self, image: List[List[int]], sr: int, sc: int, newColor: int) -> List[List[int]]:
        self.rows = len(image)
        self.cols = len(image[0])
        self.old_color = image[sr][sc]
        self.new_color = newColor
        self.image = image
        self.visited = [[0 for _ in range(self.cols)] for _ in range(self.rows)]
        self.paint([(sr, sc)])
        return self.image
    
    def paint(self, points): 
        for (i, j) in points:
            if 0 <= i < self.rows and 0 <= j < self.cols:
                if self.image[i][j] == self.old_color and not self.visited[i][j]:
                    self.visited[i][j] = 1
                    self.image[i][j] = self.new_color
                    directions = [(-1,0), (1,0), (0, -1), (0, 1)]
                    self.paint([(i + di, j + dj) for di, dj in directions])
```

