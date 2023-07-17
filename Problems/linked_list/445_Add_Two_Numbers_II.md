### [445. Add Two Numbers II](https://leetcode.com/problems/add-two-numbers-ii/)

You are given two __non-empty__ linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

__Example 1:__

<img src="https://assets.leetcode.com/uploads/2021/04/09/sumii-linked-list.jpg"></img>
```bash
Input: l1 = [7,2,4,3], l2 = [5,6,4]
Output: [7,8,0,7]
```

__Example 2:__

```bash
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [8,0,7]
```

__Example 3:__

```bash
Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [8,0,7]
```

### Solution

```python3
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        s1, s2 = [], []
        carry = 0
        head = None
        for l, s in zip([l1, l2], [s1, s2]):
            while l:
                s.append(l.val)
                l = l.next
        while s1 or s2 or carry:
            val1 = s1.pop() if s1 else 0
            val2 = s2.pop() if s2 else 0
            carry, digit = divmod(val1 + val2 + carry, 10)
            curr_node = ListNode(digit)
            curr_node.next = head
            head = curr_node
        
        return head
```
