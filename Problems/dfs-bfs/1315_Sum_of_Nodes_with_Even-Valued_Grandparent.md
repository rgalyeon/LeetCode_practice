### 1315. Sum of Nodes with Even-Valued Grandparent

Given a binary tree, return the sum of values of nodes with even-valued grandparent.  (A _grandparent_ of a node is the parent of its parent, if it exists.)

If there are no nodes with an even-valued grandparent, return 0.

__Example 1:__

<img src="https://assets.leetcode.com/uploads/2019/07/24/1473_ex1.png"></img>

<pre>
<b>Input:</b> root = [6,7,8,2,7,1,3,9,null,1,4,null,null,null,5]
<b>Output:</b> 18
<b>Explanation:</b> The red nodes are the nodes with even-value grandparent while the blue nodes are the even-value grandparents.
</pre>

__Constraints:__
* The number of nodes in the tree is between 1 and 10<sup>4</sup>.
* The value of nodes is between 1 and 100.

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
    def sumEvenGrandparent(self, root: TreeNode) -> int:
        if not root:
            return 0
        
        deq = deque()
        sum_ = 0
        
        deq.append((root, 1, 1))
        while deq:
            curr_node, father, grandfather = deq.popleft()
            if grandfather % 2 == 0:
                sum_ += curr_node.val
            if curr_node.left:
                deq.append((curr_node.left, curr_node.val, father))
            if curr_node.right:
                deq.append((curr_node.right, curr_node.val, father))
        return sum_
```
