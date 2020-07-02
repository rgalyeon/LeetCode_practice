### 1366. Rank Teams by Votes

In a special ranking system, each voter gives a rank from highest to lowest to all teams participated in the competition.

The ordering of teams is decided by who received the most position-one votes. If two or more teams tie in the first position, we consider the second position to resolve the conflict, if they tie again, we continue this process until the ties are resolved. If two or more teams are still tied after considering all positions, we rank them alphabetically based on their team letter.

Given an array of strings votes which is the `votes` of all voters in the ranking systems. Sort all teams according to the ranking system described above.

Return a string of all teams __sorted__ by the ranking system.

 

__Example 1:__
<pre>
<b>Input</b>: votes = ["ABC","ACB","ABC","ACB","ACB"]
<b>Output:</b> "ACB"
<b>Explanation</b>: Team A was ranked first place by 5 voters. No other team was voted as first place so team A is the first team.
Team B was ranked second by 2 voters and was ranked third by 3 voters.
Team C was ranked second by 3 voters and was ranked third by 2 voters.
As most of the voters ranked C second, team C is the second team and team B is the third.
</pre>

__Example 2:__

<pre>
<b>Input</b>: votes = ["WXYZ","XYZW"]
<b>Output</b>: "XWYZ"
<b>Explanation</b>: X is the winner due to tie-breaking rule. X has same votes as W for the first position but X has one vote as second position while W doesn't have any votes as second position. 
</pre>

__Example 3:__

<pre>
<b>Input</b>: votes = ["ZMNAGUEDSJYLBOPHRQICWFXTVK"]
<b>Output</b>: "ZMNAGUEDSJYLBOPHRQICWFXTVK"
<b>Explanation</b>: Only one voter so his votes are used for the ranking.
</pre>

__Example 4:__

<pre>
<b>Input</b>: votes = ["BCA","CAB","CBA","ABC","ACB","BAC"]
<b>Output</b>: "ABC"
<b>Explanation</b>: 
Team A was ranked first by 2 voters, second by 2 voters and third by 2 voters.
Team B was ranked first by 2 voters, second by 2 voters and third by 2 voters.
Team C was ranked first by 2 voters, second by 2 voters and third by 2 voters.
There is a tie and we rank teams ascending by their IDs.
</pre>

__Example 5:__

<pre>
<b>Input</b>: votes = ["M","M","M","M"]
<b>Output</b>: "M"
<b>Explanation</b>: Only team M in the competition so it has the first rank.
</pre>
 

__Constraints:__

* 1 <= `votes.length` <= 1000
* 1 <= `votes[i].length` <= 26
* `votes[i].length` == `votes[j].length` for 0 <= i, j < `votes.length`.
* `votes[i][j]` is an English upper-case letter.
* All characters of `votes[i]` are unique.
* All the characters that occur in `votes[0]` also occur in `votes[j]` where 1 <= j < votes.length.

### Solution

```Python
class Solution:
    def rankTeams(self, votes: List[str]) -> str:
        count = {team: [0] * len(votes[0]) + [team] for team in votes[0]}
        for vote in votes:
            for i, team in enumerate(vote):
                count[team][i] -= 1
        return "".join([vote[-1] for vote in sorted(count.values())])
```

