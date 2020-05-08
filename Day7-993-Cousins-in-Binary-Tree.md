<https://leetcode.com/problems/cousins-in-binary-tree/>

Use the idea of DFS to traverse the tree, find the nodes with value `x` and `y`, record their parent nodes and depths in the tree, and compare the results to see if they are at the same depth but have different parents.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right


class Solution:
    
    def isCousins(self, root: TreeNode, x: int, y: int) -> bool:
        
        def dfs(node, parent, depth, value):
            if node:
                if node.val == value:
                    return (parent, depth)
                return dfs(node.left, node, depth+1, value) or dfs(node.right, node, depth+1, value)
            
        x_parent, x_depth = dfs(root, None, 0, x)
        y_parent, y_depth = dfs(root, None, 0, y)
        return (x_depth == y_depth) and (x_parent != y_parent)
```

