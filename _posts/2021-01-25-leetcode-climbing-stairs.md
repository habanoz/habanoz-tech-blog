---
title: "Leetcode: Climbing-Stairs"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
  - Dynamic Programming
---

## Problem Description

Problem definition is taken from leetcode. 
- [Climbing-Stairs](https://leetcode.com/problems/climbing-stairs/ "Go to leetcode"){:target="_blank" rel="noopener"}

> You are climbing a staircase. It takes n steps to reach the top.

> Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top? 

### Example 1
```
Input: n = 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

### Example 2
```
Input: n = 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## Solution

Given a function of t which gives number of ways to reach nth position.
t(n) = 1
t(n-1) = 1
t(n-2) = t(n-1)+t(n)
t(n-3) = t(n-2)+t(n-1)

If t was an array element, its value would be sum of next two elements. 

Note that the array is 1 element wider to avoid range problems for t(n-1). 

Space and time complexity is O(N)

```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n==1:return 1
        table = [ 0 for i in range(0, n+2)]
        table[-2] = 1
        
        for i in range(n-1, -1, -1):
            table[i]=table[i+1]+table[i+2]

        return table[0]
    
```

