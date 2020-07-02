### 763. Partition Labels

A string `S` of lowercase English letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

__Example 1:__

<pre>
<b>Input</b>: S = "ababcbacadefegdehijhklij"
<b>Output:</b> [9,7,8]
<b>Explanation:</b>
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
</pre>
 

__Note:__

* `S` will have length in range [1, 500].
* `S` will consist of lowercase English letters (`'a'` to `'z'`) only.


### Solution

```Python
class Solution:
    def partitionLabels(self, S: str) -> List[int]:
        last_occur = {letter: idx for idx, letter in enumerate(S)}
        max_ = -1
        cnt = 0
        res = []
        
        for idx, letter in enumerate(S):
            if max_ < last_occur[letter]:
                max_ = last_occur[letter]
            cnt += 1
            if idx == max_:
                res.append(cnt)
                cnt = 0
        return res
```
