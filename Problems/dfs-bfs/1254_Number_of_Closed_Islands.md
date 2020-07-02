### [1254. Number of Closed Islands](https://leetcode.com/problems/number-of-closed-islands/)

Given a 2D `grid` consists of `0s` (land) and `1s` (water).  An island is a maximal 4-directionally connected group of `0s` and a closed island is an island totally (all left, top, right, bottom) surrounded by `1s`.

Return the number of closed islands.

__Example 1:__

<img src="https://assets.leetcode.com/uploads/2019/10/31/sample_3_1610.png"></img>

<pre>
<b>Input:</b> grid = [[1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0]]
<b>Output:</b> 2
<b>Explanation:</b> 
Islands in gray are closed because they are completely surrounded by water (group of 1s).
</pre>

__Example 2:__

<img src="https://assets.leetcode.com/uploads/2019/10/31/sample_4_1610.png"></img>

<pre>
<b>Input:</b> grid = [[0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0]]
<b>Output:</b> 1
</pre>

__Example 3:__

<pre>
<b>Input:</b> grid = [[1,1,1,1,1,1,1],
               [1,0,0,0,0,0,1],
               [1,0,1,1,1,0,1],
               [1,0,1,0,1,0,1],
               [1,0,1,1,1,0,1],
               [1,0,0,0,0,0,1],
               [1,1,1,1,1,1,1]]
<b>Output:</b> 2
</pre>

### Solution

```Python
class Solution:
    def closedIsland(self, grid: List[List[int]]) -> int:
        n_isl = 0
        
        def dfs(i, j):
            if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] != 0:
                return 
            
            grid[i][j] = 1
            dfs(i + 1, j)
            dfs(i - 1, j)
            dfs(i, j + 1)
            dfs(i, j - 1)
        
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if (i == 0 or i == len(grid) - 1 or j == 0 or j == len(grid[0]) - 1) and grid[i][j] == 0:
                    dfs(i, j)
        
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 0:
                    dfs(i, j)
                    n_isl += 1
        return n_isl
```
