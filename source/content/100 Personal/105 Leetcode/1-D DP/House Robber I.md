#DyanimcProgramming #spaceoptimzied
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** 4
**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

**Example 2:**

**Input:** nums = [2,7,9,3,1]
**Output:** 12
**Explanation:** Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.

## Brute force intuition

You can have a tree starting at each index and then just go to the max between the next house and current + next-to-next house

![[Pasted image 20250228111330.png]]

## Optimal solution

Instead of having to redo the work, we store the maxes in two variables as we iterate through

```
class Solution:

    def rob(self, nums: List[int]) -> int:

        rob1, rob2 = 0, 0

  

        # [rob1, rob2, n, n+1, ...]

        for num in nums:

            temp = max(rob2, num + rob1)

            rob1 = rob2

            rob2 = temp

        return rob2
```

## Key intuition

Like the other DP problems, start with the brute force approach then find the key recursive function. You can then use this to identify the repeated work and hwo you can eliminate it with DP, easiest seems to be with two variables 

Most often you are just iterating and looking at the next two values and just stacking up the subproblems until you've solved the big problem