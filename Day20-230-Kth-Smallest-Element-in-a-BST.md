https://leetcode.com/problems/kth-smallest-element-in-a-bst/

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right


class Solution:

    def kthSmallest(self, root: TreeNode, k: int) -> int:
        self.k = k
        self.res = None
        self.in_order(root)
        return self.res
        
    def in_order(self, node: TreeNode):
        if (self.k <= 0) or (not node):
            return
        self.in_order(node.left)
        if self.k == 1:
            self.res = node.val
            self.k = -1
            return
        self.k -= 1
        if self.k > 0:
            self.in_order(node.right)
        
```

