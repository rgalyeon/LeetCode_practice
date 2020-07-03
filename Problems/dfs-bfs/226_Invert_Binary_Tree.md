### [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

Invert a binary tree.

__Example:__

<pre>
<b>Input:</b>

     4
   /   \
  2     7
 / \   / \
1   3 6   9

<b>Output:</b>

     4
   /   \
  7     2
 / \   / \
9   6 3   1

</pre>

__Trivia:__
This problem was inspired by this original tweet by Max Howell:

> Google: 90% of our engineers use the software you wrote (Homebrew), but you can’t invert a binary tree on a whiteboard so f*** off.

### Solution

```Python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

from collections import deque

class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:
            return None
        
        deq = deque()
        
        deq.append(root)
        while deq:
            node = deq.popleft()
            node.left, node.right = node.right, node.left
            if node.left:
                deq.append(node.left)
            if node.right:
                deq.append(node.right)
        return root
```
