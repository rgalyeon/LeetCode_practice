### [49. Group Anagrams](https://leetcode.com/problems/group-anagrams/)

Given an array of strings, group anagrams together.

__Example:__

<pre>
<b>Input:</b> ["eat", "tea", "tan", "ate", "nat", "bat"],
<b>Output:</b>
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
</pre>

__Note:__

* All inputs will be in lowercase.
* The order of your output does not matter.

### Solution

```Python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        group_dict = defaultdict(list)
        
        for word in strs:
            char_freq = [0] * 26
            for char in word:
                char_freq[ord(char) - ord('a')] += 1
            group_dict[tuple(char_freq)].append(word)
        return group_dict.values()
```
