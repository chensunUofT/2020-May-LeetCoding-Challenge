<https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/>

Firstly, it is obvious that the first node is the root of the BST.  
Then, we iterate over the array, **use a stack to store the nodes that might potentially have children nodes in the tree**, and find where each node should be added into the tree:  

- If the value of the new node is smaller than the previous node in the stack, then the new node is the left child of the previous node, and the new node needs to be pushed into the stack
- If the value of the new node is bigger than previous, then it should be **the right child of the previous node or one of its ancestors**. To find the parent of the new node, keep popping the last node in the stack (since it won't have left or right child) until either we find a node with greater value than the new node or the stack get empty; in either circumstance, the last popped node is the parent of the new node.  

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> TreeNode:
        if not preorder:
            return None
        root = TreeNode(preorder[0])
        stack = [root]
        for num in preorder[1:]:
            new_node = TreeNode(num)
            if num < stack[-1].val:
                stack[-1].left = new_node
                stack.append(new_node)
            else:
                while stack and num > stack[-1].val:
                    last_node = stack.pop()
                last_node.right = new_node
                stack.append(new_node)
        return root
```



