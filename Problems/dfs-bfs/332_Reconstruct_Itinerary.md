### [332. Reconstruct Itinerary](https://leetcode.com/problems/reconstruct-itinerary/)

Given a list of airline tickets represented by pairs of departure and arrival airports `[from, to]`, reconstruct the itinerary in order.
All of the tickets belong to a man who departs from `JFK`.
Thus, the itinerary must begin with `JFK`.

__Note:__
1. If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
2. All airports are represented by three capital letters (IATA code).
3. You may assume all tickets form at least one valid itinerary.
4. One must use all the tickets once and only once.

__Example 1:__

<pre>
<b>Input:</b> [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
<b>Output:</b> ["JFK", "MUC", "LHR", "SFO", "SJC"]
</pre>

__Example 2:__

<pre>
<b>Input:</b> [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
<b>Output:</b> ["JFK","ATL","JFK","SFO","ATL","SFO"]
<b>Explanation:</b> Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"]. But it is larger in lexical order.
</pre>

### Solution

```Python
from collections import defaultdict

class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        graph = defaultdict(list)
        itinerary = []
        stack = ['JFK']
        
        tickets.sort(reverse=True)
        for from_, to in tickets:
            graph[from_].append(to)
        while stack:
            while arr_airports := graph[stack[-1]]:
                stack.append(arr_airports.pop())
            itinerary.append(stack.pop())
        return reversed(itinerary)
```

