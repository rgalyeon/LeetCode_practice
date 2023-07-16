### [1125. Smallest Sufficient Team](https://leetcode.com/problems/smallest-sufficient-team/)

In a project, you have a list of required skills `req_skills`, and a list of `people`. The ith person `people[i]` contains a list of skills that the person has.

Consider a sufficient team: a set of people such that for every required skill in req_skills, there is at least one person in the team who has that skill. We can represent these teams by the index of each person.

    For example, team = [0, 1, 3] represents the people with skills people[0], people[1], and people[3].

Return any sufficient team of the smallest possible size, represented by the index of each person. You may return the answer in __any order__.

It is __guaranteed__ an answer exists.

__Example 1:__

```bash
Input: req_skills = ["java","nodejs","reactjs"], people = [["java"],["nodejs"],["nodejs","reactjs"]]
Output: [0,2]
```

__Example 2:__

```bash
Input: req_skills = ["algorithms","math","java","reactjs","csharp","aws"], people = [["algorithms","math","java"],["algorithms","math","reactjs"],["java","csharp","aws"],["reactjs","csharp"],["csharp","math"],["aws","java"]]
Output: [1,2]
```

__Constraints:__

* `1 <= req_skills.length <= 16`
* `1 <= req_skills[i].length <= 16`
* `req_skills[i]` consists of lowercase English letters.
* All the strings of req_skills are __unique__.
* `1 <= people.length <= 60`
* `0 <= people[i].length <= 16`
* `1 <= people[i][j].length <= 16`
* `people[i][j]` consists of lowercase English letters.
* All the strings of `people[i]` are unique.
* Every skill in `people[i]` is a skill in req_skills.
* It is __guaranteed__ a sufficient team exists.


### Solution

```python3
def smallestSufficientTeam(self, req_skills: List[str], people: List[List[str]]) -> List[int]:
    # skills num representation
    skills_num = {skill: i for i, skill in enumerate(req_skills)}

    # convert cadidates' skills to a binary representation
    people_conv = []
    for guy_skills in people:
        bit_skills = 0
        for skill in guy_skills:
            bit_skills |= 1 << skills_num[skill]
        people_conv.append(bit_skills)
    
    @cache
    def dp(guy_i, bit_mask):
        if bit_mask == (1 << len(req_skills)) - 1:
            return []
        if guy_i == len(people):
            return [0] * 61

        # compare a solution that includes person guy_i and a solution that doesn't
        return min([dp(guy_i+1, bit_mask), [guy_i] + dp(guy_i+1, bit_mask | people_conv[guy_i])], key=len)
    
    return(dp(0, 0))
```
