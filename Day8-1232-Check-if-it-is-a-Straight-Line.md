<https://leetcode.com/problems/check-if-it-is-a-straight-line/>

Use the coordinates of the first two points to calculate a `direction` vector, and use the cross product of a new vector and the `direction` vector to check if they are collinear.

```python
class Solution:
    def checkStraightLine(self, coordinates: List[List[int]]) -> bool:
        
        def vec_diff(v1, v2):
            return [v1[0]-v2[0], v1[1]-v2[1]]
        
        def vec_cross_product(v1, v2):
            return v1[0] * v2[1] - v1[1] * v2[0]
        
        if len(coordinates) < 3:
            return True
        else:
            direction = vec_diff(coordinates[1], coordinates[0])
            for i in range(2, len(coordinates)):
                if vec_cross_product(direction, vec_diff(coordinates[i], coordinates[0])):
                    return False
            return True
```

Or, calculate the slope of the line determined by every adjacent points pair, and check if all of the slopes are equal. 

```python
class Solution:
    def checkStraightLine(self, coordinates: List[List[int]]) -> bool:
        
        def slope(a, b):
            return (b[1] - a[1]) / (b[0] - a[0]) if b[0] - a[0] else float("inf")
        
        if len(coordinates) < 3:
            return True
        
        k = slope(coordinates[0], coordinates[1])
        for i in range(2, len(coordinates)):
            if slope(coordinates[i-1], coordinates[i]) != k:
                return False
        return True
```

