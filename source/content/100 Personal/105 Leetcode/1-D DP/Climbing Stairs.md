#DyanimcProgramming #spaceoptimzed
You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**
``
**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

**Example 2:**

**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step


## Brute force Intuition and Solution

At each step there are 2 options you could take, 1 or 2 steps. So you can use recursion to find all the paths that lead to n. 

This is a 2^n solution and will exceed time limit at higher N's

The problem is we are doing a lot of repeated work when calculating the paths 

![[Pasted image 20250228091741.png]]

There is so much wasted work here, as you can see there are repeated subtree for 2, 3, and 4 which we recalculate everytime we go through that path

## Optimal Solution

We use a bottom up approach to solving this, and its simple

We have an array of, n=5 size n + 1, and start at the end

at i = 4, there's only 1 step you can take so the array currently is 

`[_ , _, _, _, _, 1]`

at i = 3, there's only 1 step you can take so that you stay inbounds

`[_, _ , _, _, 1, 1]`

at i = 2, now there are 2 steps you can take, and all we have to do is count up how many steps it takes to get to the end after we take a step. 

at i = 2, you can go to i = 3 or i =4, from i = 3 you take 1 step to get to the end and the same for i = 4, so i2 = i3 + i4

`[_, _ , _, 2, 1, 1]`

now at i = 1, I can take 2 steps. to i2 or i3. From i2, there are two ways to get to the end and at i3 there is 1 way to get to the end. So at i1 there are i2 + i3 ways to get to the end (3)

`[_, _ , 3, 2, 1, 1]`

we know the drill by now so 

`[8, 5 , 3, 2, 1, 1]`

### Concepts to look out for

I found the brute force solution quite quickly, but didn't pick up on the exact reasons that was making it redundant. Looking for and identifying those pieces that require repeated work would help lead me to the optimal solution. 