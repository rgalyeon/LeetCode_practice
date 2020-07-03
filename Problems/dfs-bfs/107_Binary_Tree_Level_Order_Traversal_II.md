### 107. Binary Tree Level Order Traversal II

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

__For example:__
Given binary tree `[3,9,20,null,null,15,7]`,

<pre>
    3
   / \
  9  20
    /  \
   15   7

</pre>

return its bottom-up level order traversal as:

<pre>

[
  [15,7],
  [9,20],
  [3]
]
</pre>

### Solution

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

from collections import deque

class Solution:            
        def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
            if not root:
                return []
            
            res = []
            deq = deque()
            
            deq.append(root)
            while deq:
                res.append([])
                for i in range(len(deq)):
                    node = deq.popleft()
                    res[-1].append(node.val)
                    if node.left:
                        deq.append(node.left)
                    if node.right:
                        deq.append(node.right)
            return reversed(res)
```
