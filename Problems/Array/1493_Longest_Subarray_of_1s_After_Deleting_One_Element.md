### 1493. Longest Subarray of 1's After Deleting One Element

Given a binary array nums, you should delete one element from it.

Return the size of the longest non-empty subarray containing only 1's in the resulting array.

Return 0 if there is no such subarray.

 

__Example 1:__

<pre>
<b>Input:</b> nums = [1,1,0,1]
<b>Output:</b> 3
<b>Explanation:</b> After deleting the number in position 2, [1,1,1] contains 3 numbers with value of 1's.
</pre>

__Example 2:__

<pre>
<b>Input:</b> nums = [0,1,1,1,0,1,1,0,1]
<b>Output</b>: 5
<b>Explanation</b>: After deleting the number in position 4, [0,1,1,1,1,1,0,1] longest subarray with value of 1's is [1,1,1,1,1].
</pre>

__Example 3:__

<pre>
<b>Input:</b> nums = [1,1,1]
<b>Output:</b> 2
<b>Explanation:</b> You must delete one element.
</pre>

__Example 4:__

<pre>
<b>Input:</b> nums = [1,1,0,0,1,1,1,0,1]
<b>Output:</b> 4
</pre>

__Example 5:__

<pre>
<b>Input:</b> nums = [0,0,0]
<b>Output:</b> 0
</pre>
 

__Constraints:__

* 1 <= nums.length <= 10^5
* nums[i] is either 0 or 1.

### Solution

```Python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        if all(nums):
            return len(nums) - 1
        ignored, notignored, max_ = 0, 0, 0
        
        for num in nums:
            if num == 1:
                ignored += num
                notignored += num
            else:
                max_ = max(ignored, max_)
                ignored = notignored
                notignored = 0
        max_ = max(ignored, max_)
        return max_
```
