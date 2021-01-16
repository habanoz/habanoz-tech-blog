---
title: "Leetcode: Unique Paths"
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
- [Unique Paths](https://leetcode.com/problems/unique-paths/ "Go to leetcode"){:target="_blank" rel="noopener"}

> A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

> The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

> How many possible unique paths are there?

### Example 1
![robot_maze](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
Input: m = 3, n = 7
Output: 28
```

### Example 2
```
Input: m = 7, n = 3
Output: 28
```

## Solution

Dynamic solution requires a mxn matrix to keep track of cell visits. Thus solutions space complexity is O(mxn)

Target cell is set to 1. Starting from target cell upper and left cells values are incremented by current cell value.
Time complexity is O(mxn).

|  <!-- -->  | <!-- --> | <!-- --> | <!-- --> |
|----|----|---|---|
| 0  | 10 | 4 | 1 |
| 10 | 6  | 3 | 1 |
| 4  | 3  | 2 | 1 |
| 1  | 1  | 1 | 1 |

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        grid = [[0 for j in range(n)] for i in range(m)]
        grid[m-1][n-1]=1
        for i in range(m-1, -1, -1):
            for j in range(n-1, -1, -1):
                self.step(grid, i, j)
        return grid[0][0]
    
    def step(self, grid, i,j):
        count = grid[i][j]
        
        if j>0:
            grid[i][j-1]+=count
        if i>0:
            grid[i-1][j]+=count
```

