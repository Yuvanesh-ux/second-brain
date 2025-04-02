Given an `m x n` integers `matrix`, return _the length of the longest increasing path in_ `matrix`.

From each cell, you can either move in four directions: left, right, up, or down. You **may not** move **diagonally** or move **outside the boundary** (i.e., wrap-around is not allowed).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/05/grid1.jpg)

**Input:** matrix = [[9,9,4],[6,6,8],[2,1,1]]
**Output:** 4
**Explanation:** The longest increasing path is `[1, 2, 6, 9]`.

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/27/tmp-grid.jpg)

**Input:** matrix = [[3,4,5],[3,2,6],[2,2,1]]
**Output:** 4
**Explanation:** The longest increasing path is `[3, 4, 5, 6]`. Moving diagonally is not allowed.

**Example 3:**

**Input:** matrix = [[1]]
**Output:** 1

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 200`
- `0 <= matrix[i][j] <= 231 - 1`

## Key Intuition

The key thing is to first discover that you will probably have to do dfs from every cell in the grid and then run the algorithm of going to the squares that have a higher val and recording the length. 

The way to optimize is by storing the longest possible path at any given cell and using that cached values so you dont have to recompute a path that has already been computed.

## Solution

```
class Solution(object):

    def longestIncreasingPath(self, matrix):

        """

        :type matrix: List[List[int]]

        :rtype: int

        """

        ROWS, COLS = len(matrix), len(matrix[0])

        dp = {} # (r, c) : LIP

  

        def dfs(r, c, prevVal):

            if (r == ROWS or c == COLS or

                r < 0 or c < 0 or

                matrix[r][c] <= prevVal):

                return 0

            if (r, c) in dp:

                return dp[(r, c)]

  

            res = 1

            res = max(res, 1 + dfs(r + 1, c, matrix[r][c]))

            res = max(res, 1 + dfs(r - 1, c, matrix[r][c]))

            res = max(res, 1 + dfs(r, c + 1, matrix[r][c]))

            res = max(res, 1 + dfs(r, c - 1, matrix[r][c]))

            dp[(r, c)] = res

  

            return res

  

        for r in range(ROWS):

            for c in range(COLS):

                dfs(r, c, -1)

  

        return max(dp.values())
```