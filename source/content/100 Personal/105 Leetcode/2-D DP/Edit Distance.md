Given two strings `word1` and `word2`, return _the minimum number of operations required to convert `word1` to `word2`_.

You have the following three operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

**Example 1:**

**Input:** word1 = "horse", word2 = "ros"
**Output:** 3
**Explanation:** 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

**Example 2:**

**Input:** word1 = "intention", word2 = "execution"
**Output:** 5
**Explanation:** 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')

**Constraints:**

- `0 <= word1.length, word2.length <= 500`
- `word1` and `word2` consist of lowercase English letters.

## Key intuition

Same as with other DP problems, the key to figuring out how to solve is to first find the recursive solution and try to memoize it. The recursive solution is to just have two pointers on each word, and if they dont match up, you have three separate decision paths you can go down to stumble on the answer. 

With a top-down approach, you can cache the recursive paths and you dont have to redo a lot of the work

## Solution

```
class Solution(object):

    def minDistance(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        m, n = len(word1), len(word2)
        cache = {}

        def dfs(i, j):
            if i == m:
                return n - j
            if j == n:
                return m - i
            if (i, j) in cache:
                return cache[(i, j)]
            if word1[i] == word2[j]:
                cache[(i, j)] = dfs(i + 1, j + 1)
            else:
                res = min(dfs(i + 1, j), dfs(i, j + 1))
                res = min(res, dfs(i + 1, j + 1))
                cache[(i, j)] = 1 + res
                
            return cache[(i, j)]
            
        return dfs(0, 0)
```