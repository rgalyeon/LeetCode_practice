### 11. Container With Most Water

Given `n` non-negative integers a<sub>1</sub>, a<sub>2</sub>, ..., a<sub>n</sub> , where each represents a point at coordinate (i, a<sub>i</sub>).
`n` vertical lines are drawn such that the two endpoints of line i is at (i, a<sub>i</sub>) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

__Note:__ You may not slant the container and n is at least 2.

<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg"></img>

__Example:__

<pre>
<b>Input:</b> [1,8,6,2,5,4,8,3,7]
<b>Output:</b> 49
</pre>

### Solution

```Python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        max_area = 0
        
        while left != right:
            res = min(height[left], height[right]) * (right - left)
            if res > max_area:
                max_area = res
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return max_area
```
