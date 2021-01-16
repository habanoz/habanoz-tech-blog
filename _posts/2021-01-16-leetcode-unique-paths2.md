---
title: "Leetcode: Unique Paths 2"
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
- [Unique Paths 2](https://leetcode.com/problems/unique-paths-ii/ "Go to leetcode"){:target="_blank" rel="noopener"}

> A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

> The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

> Now consider if some obstacles are added to the grids. How many unique paths would there be?

> An obstacle and space is marked as 1 and 0 respectively in the grid.

For Unique Paths 1 problem visit [Unique Paths 1]({{ site.baseurl }}{% post_url 2021-01-16-leetcode-unique-paths %})

### Example 1
![robot_maze](https://assets.leetcode.com/uploads/2020/11/04/robot1.jpg)
```
Input: obstacleGrid = [[0,0,0],[0,1,0],[0,0,0]]
Output: 2
Explanation: There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```

### Example 2
![robot_maze](https://assets.leetcode.com/uploads/2020/11/04/robot2.jpg)
```
Input: obstacleGrid = [[0,1],[0,0]]
Output: 1
```

## Solution

Solution is similar to [Unique Paths 1]({{ site.baseurl }}{% post_url 2021-01-16-leetcode-unique-paths %}).

In order not to confuse with obstacle values, target value is set to 2. As a result each path is counted twice and 
in the end result is divided by 2. Also obstacle values are not propagated.

No extra space is used. 
Time complexity is O(mxn).

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        grid = obstacleGrid
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        
        if grid[m-1][n-1]==1 or grid[0][0]==1:
            return 0
        
        grid[m-1][n-1]=2
        for i in range(m-1, -1, -1):
            for j in range(n-1, -1, -1):
                self.step(grid, i, j)
        return int(grid[0][0]/2)
    
    def step(self, grid, i,j):
        count = grid[i][j]
        if count%2==1:
            return 
        
        if j>0:
            grid[i][j-1]+=count
        if i>0:
            grid[i-1][j]+=count
```

