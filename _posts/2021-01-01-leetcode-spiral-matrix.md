---
title: "Leetcode: Spiral Matrix"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
---

## Problem Description

Problem definition is taken from leetcode. 
- [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given an m x n matrix, return all elements of the matrix in spiral order.


### Example 1 
```
![Example1](https://assets.leetcode.com/uploads/2020/11/13/spiral1.jpg)

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

### Example 2
```
![Example2](https://assets.leetcode.com/uploads/2020/11/13/spiral.jpg)

Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```

## Solution

Solution involves depth-first search and backtracking. 

The approach uses the fact that the spiral traversal requires change in only one axis. Given a matrix having i rows and j columns, at any step either i axis or j axis changes. 
Another fact is change axis and direction does not change until a corner is reached. 

There are two kinds of corners: actual and visited. 
- Actual corners are invalid matrix indices. For example i or j indices cannot be less than zero.
- Visited corners are matrix elements that are already visited. The solution requires the visited matrix elements are marked with value None.  


```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        result=[]
        self.df(matrix, 0, -1, 0, 1, result, 0)
        return result
    
    def df(self, m, i,j,di,dj, result, marked):
        ni=len(m)
        nj=len(m[0])
        
        # print("df", i, j,"d",di,dj)
        
        if marked == ni*nj:
            return
        
        ip = i+di
        jp = j+dj
        
        if ip>=ni or ip<0 or (di!=0 and m[ip][jp] is None):
            ddi, ddj = self.on_spiral_corner(di, dj)
            return self.df(m, i, j, ddi, ddj, result, marked)
        
        if jp>=nj or jp<0 or (dj!=0 and m[ip][jp] is None):
            ddi, ddj = self.on_spiral_corner(di, dj)
            return self.df(m, i, j, ddi, ddj, result, marked)
        
        self.add(m, ip, jp, result)
        
        return self.df(m, ip, jp, di, dj, result, marked+1)
      
    def on_spiral_corner(self, di,dj):
        if di > 0 or di < 0:
            return 0, -di
        
        if dj > 0 or dj < 0:
            return dj, 0
        
    
    def add(self, m, i, j, result):
        # print(i,j,"-", m[i][j])
        
        val = m[i][j]
        m[i][j]=None
        result.append(val)

```

