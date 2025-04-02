#DyanimcProgramming #memoization
You are given an integer array `nums` and an integer `target`.

You want to build an **expression** out of nums by adding one of the symbols `'+'` and `'-'` before each integer in nums and then concatenate all the integers.

- For example, if `nums = [2, 1]`, you can add a `'+'` before `2` and a `'-'` before `1` and concatenate them to build the expression `"+2-1"`.

Return the number of different **expressions** that you can build, which evaluates to `target`.

**Example 1:**

**Input:** nums = [1,1,1,1,1], target = 3
**Output:** 5
**Explanation:** There are 5 ways to assign symbols to make the sum of nums be target 3.
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3

**Example 2:**

**Input:** nums = [1], target = 1
**Output:** 1

**Constraints:**

- `1 <= nums.length <= 20`
- `0 <= nums[i] <= 1000`
- `0 <= sum(nums[i]) <= 1000`
- `-1000 <= target <= 1000`

## Key intuition

The key intuition is first 

1. Find the recursive/bruteforce case
2. Find how to use memoization to optimize it

Usually just memoization should be efficient enough to pass any interview. Memoization usually consists of using a hashmap to map the current state to the answer we want to get to, and by the time the backtracking is done the final state should have our answer. 

## Solution



```
class Solution:

    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        cache = {} # (index : #of ways)
        
        def backtrack(i, cur_sum):
            if i == len(nums):
                return 1 if cur_sum == target else 0
            if (i, cur_sum) in cache:
                return cache[(i, cur_sum)]

            cache[(i, cur_sum)] = backtrack(i + 1, cur_sum + nums[i]) + backtrack(i + 1, cur_sum - nums[i])

            return cache[(i, cur_sum)]

        return backtrack(0, 0)
```