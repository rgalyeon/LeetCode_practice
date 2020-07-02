### 986. Interval List Intersections

Given two lists of __closed__ intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

(Formally, a closed interval `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.  
The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.
For example, the intersection of [1, 3] and [2, 4] is [2, 3].)

__Example 1:__

<img src="https://assets.leetcode.com/uploads/2019/01/30/interval1.png"></img>

<pre>
<b>Input:</b> A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
<b>Output:</b> [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
</pre>
 

__Note:__

* `0 <= A.length < 1000`
* `0 <= B.length < 1000`
* `0 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9`


### Solution

```Python
class Solution:
    def intervalIntersection(self, A: List[List[int]], B: List[List[int]]) -> List[List[int]]:
        i = j = 0
        res = []
        
        while i < len(A) and j < len(B):
            if B[j][0] <= A[i][1] and B[j][1] >= A[i][0]:
                res.append((max(A[i][0], B[j][0]), min(A[i][1], B[j][1])))
            if A[i][1] < B[j][1]:
                i += 1
            else:
                j += 1
        return res
```
