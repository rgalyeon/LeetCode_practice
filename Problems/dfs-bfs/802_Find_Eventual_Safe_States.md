### [802. Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/)

There is a directed graph of n nodes with each node labeled from `0` to `n - 1`. The graph is represented by a __0-indexed__ 2D integer array `graph` where `graph[i]` is an integer array of nodes adjacent to node i, meaning there is an edge from node i to each node in graph[i].

A node is a __terminal node__ if there are no outgoing edges. A node is a __safe node__ if every possible path starting from that node leads to a __terminal node__ (or another safe node).

Return an array containing all the __safe nodes__ of the graph. The answer should be sorted in __ascending__ order.

__Example 1:__

<img src="https://s3-lc-upload.s3.amazonaws.com/uploads/2018/03/17/picture1.png"></img>
<pre>
<b>Input:</b> graph = [[1,2],[2,3],[5],[0],[5],[],[]]
<b>Output:</b> [2,4,5,6]
Explanation: The given graph is shown above.
Nodes 5 and 6 are terminal nodes as there are no outgoing edges from either of them.
Every path starting at nodes 2, 4, 5, and 6 all lead to either node 5 or 6.
</pre>

__Constraints:__

* `n == graph.length`
* `1 <= n <= 10^4`
* `0 <= graph[i].length <= n`
* `0 <= graph[i][j] <= n - 1`
* `graph[i]` is sorted in a strictly increasing order.
* The graph may contain self-loops.
* The number of edges in the graph will be in the range [1, 4 * 10^4].


### Solution

```python
class Solution:
    def eventualSafeNodes(self, graph: List[List[int]]) -> List[int]:
        status = [0] * len(graph)
        
        def dfs(node):
            if status[node] == 1:
                return True
            if status[node] == 2:
                return False
            status[node] = 1
            for i in graph[node]:
                if dfs(i):
                    return True
            status[node] = 2
            return False
        
        return [i for i in range(len(graph)) if not dfs(i)]
```
