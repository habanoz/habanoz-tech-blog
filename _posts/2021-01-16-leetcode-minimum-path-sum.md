---
title: "Leetcode: Minimum Path Sum"
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
- [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

> Note: You can only move either down or right at any point in time.

For Unique Paths 1 problem visit [Unique Paths 1]({{ site.baseurl }}{% post_url 2021-01-16-leetcode-unique-paths %})

### Example 1
![grid](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)
```
Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
```

### Example 2
```
Input: grid = [[1,2,3],[4,5,6]]
Output: 12
```

## Solution

Solution is similar to [Unique Paths 1]({{ site.baseurl }}{% post_url 2021-01-16-leetcode-unique-paths %}).

However, instead of summing number of cells in a path, cost of the cells in a path are computed.
A separate grid is needed to make computations. Starting from target cell, Given a cell, neighbour (left or up) 
values are updated if not previously computed or there is a cheaper path available.

Copy of the grid is needed. Thus space complexity is O(mXn)
Time complexity is O(mxn).

```python
class Solution:
    def minPathSum(self, grid: List[List[int]]) -> int:
        m = len(grid)
        n = len(grid[0])
        
        if m==1 or n==1:
            return sum(sum(row)for row in grid)
        
        newGrid = [[None for j in range(n)] for i in range(m)]
        newGrid[m-1][n-1]=grid[m-1][n-1]
        
        for i in range(m-1, -1, -1):
            for j in range(n-1, -1, -1):
                self.step(grid, newGrid,  i, j)
        
        return min(newGrid[0][1], newGrid[1][0])+grid[0][0]
    
    def step(self, grid, newGrid, i,j):
        cost = newGrid[i][j] or grid[i][j]
        
        if j>0 and (newGrid[i][j-1] is None or newGrid[i][j-1]>cost+grid[i][j-1]):
            newGrid[i][j-1]=cost+grid[i][j-1]
            
        if i>0 and (newGrid[i-1][j] is None or newGrid[i-1][j]>cost+grid[i-1][j]):
            newGrid[i-1][j]=cost+grid[i-1][j]
```

