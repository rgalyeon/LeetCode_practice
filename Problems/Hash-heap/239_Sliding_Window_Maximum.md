### [239. Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

Given an array `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right.
You can only see the `k` numbers in the window. Each time the sliding window moves right by one position. Return the max sliding window.

__Follow up:__
Could you solve it in linear time?

__Example:__

<pre>
<b>Input:</b> nums = [1,3,-1,-3,5,3,6,7], and k = 3
<b>Output:</b> [3,3,5,5,6,7] 
<b>Explanation:</b> 

Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       <b>3</b>
 1 [3  -1  -3] 5  3  6  7       <b>3</b>
 1  3 [-1  -3  5] 3  6  7       <b>5</b>
 1  3  -1 [-3  5  3] 6  7       <b>5</b>
 1  3  -1  -3 [5  3  6] 7       <b>6</b>
 1  3  -1  -3  5 [3  6  7]      <b>7</b>
</pre>
 

__Constraints:__

* 1 <= nums.length <= 10<sup>5</sup>
* -10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>
* 1 <= k <= nums.length

### Solution

```Python
from collections import deque

class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        deq = deque()
        res = []
        for i, num in enumerate(nums):
            
            while deq and num > nums[deq[-1]]:
                deq.pop()
            deq.append(i)
            if i - k + 1 >= 0:
                res.append(nums[deq[0]])
            if i - k + 1 >= 0 and deq[0] == i - k + 1:
                deq.popleft()
            
        return res
```
