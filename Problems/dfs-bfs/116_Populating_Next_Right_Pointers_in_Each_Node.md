### 116. Populating Next Right Pointers in Each Node

You are given a __perfect binary tree__ where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

```Python
class Node:
    def __init__(self, val: int = 0, left: 'Node' = None, right: 'Node' = None, next: 'Node' = None):
        self.val = val
        self.left = left
        self.right = right
        self.next = next
```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

__Follow up:__

* You may only use constant extra space.
* Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

__Example 1:__

<img src="https://assets.leetcode.com/uploads/2019/02/14/116_sample.png"></img>

<pre>
<b>Input:</b> root = [1,2,3,4,5,6,7]
<b>Output:</b> [1,#,2,3,#,4,5,6,7,#]
<b>Explanation:</b> Given the above perfect binary tree (Figure A), your function should populate each next pointer to point
to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers,
with '#' signifying the end of each level.
</pre>

__Constraints:__

* The number of nodes in the given tree is less than `4096`.
* `-1000 <= node.val <= 1000`

### Solution

```Python
class Solution:
    def connect(self, root: 'Node') -> 'Node':
        head = root
        while root and root.left:
            next_ = root.left
            while root:
                root.left.next = root.right
                root.right.next = root.next and root.next.left
                root = root.next
            root = next_
        return head
```
