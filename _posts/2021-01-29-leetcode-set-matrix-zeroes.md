---
title: "Leetcode: Set Matrix Zeroes"
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
- [Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given an m x n matrix. If an element is 0, set its entire row and column to 0. Do it in-place.

> Follow up:
> - A straight forward solution using O(mn) space is probably a bad idea.
> - A simple improvement uses O(m + n) space, but still not the best solution.
> - Could you devise a constant space solution?

### Example 1
![example1](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)
```
Input: matrix = [[1,1,1],[1,0,1],[1,1,1]]
Output: [[1,0,1],[0,0,0],[1,0,1]]
```

### Example 2
![example2](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)
```
Input: matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]
Output: [[0,0,0,0],[0,4,5,0],[0,3,1,0]]
```


## Solution 1

First approach uses bit manipulation keep track of rows and columns having value 0.
For example if matrix[i][j]==0, then i'th bit in rows and j'th bit cols variables are set to 1.

In seconds iteration those marked rows and columns are filled with zeros. single_loop and double_loop methods do the 
same task. double_loop version works slightly faster which is surprising.

Time complexity is O(mxn). Space complexity is O(1). A space which is large enough to store 14 integers is enough to make the bit manipulation. 

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        cols=2**201
        rows=2**201
        
        n = len(matrix)
        m = len(matrix[0])
        
        for i in range(n):
            for j in range(m):
                if matrix[i][j]==0:
                    rows = rows | 2**i
                    cols = cols | 2**j
        
        # self.single_loop(matrix, n, m, cols, rows)
        self.double_loop(matrix, n, m, cols, rows)
        

    def single_loop(self, matrix, n, m, cols, rows):     
        for i in range(n):
            for j in range(m):
                if rows & 2**i or cols & 2**j:
                    matrix[i][j]=0
                    
    def double_loop(self, matrix, n, m, cols, rows):
        
        for i in range(n):
            if rows & 2**i:
                for j in range(m):
                    matrix[i][j]=0
        
        for j in range(m):
            if cols & 2**j:
                for i in range(n):
                    matrix[i][j]=0        
```

# Solution 2

Second approach uses first row and first column to trace zeros. This approach does not need any extra space other than two boolean variables. In fact, only one of them is necessary.

matrix[0][0] is used as marker for the first row.
first_col_marked variable is used as marker for the first column.

In this configuration, first row and first column ,excluding the index [0,0], can be used as marker space.

if matrix[i][j]==0 then matrix[i][0] and matrix[0][j] is set to 0. Note that matrix[i][0] can point to matrix[0][0]. 

At the end the first row and column is filled with zeros if necessary.

Space complexity is O(1) and time complexity is O(mxn).

```python
class Solution:
    def setZeroes(self, matrix: List[List[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        
        n = len(matrix)
        m = len(matrix[0])
        
        first_col_marked=False
        first_row_marked=False
        
        for i in range(n):
            if matrix[i][0]==0:
                first_col_marked = True
                
            for j in range(1, m):
                if matrix[i][j]==0:
                    matrix[i][0]=0
                    matrix[0][j]=0
        
        first_row_marked = matrix[0][0]==0
        
        for i in range(1, n):
            for j in range(1, m):
                if matrix[i][0]==0 or matrix[0][j]==0:
                    matrix[i][j]=0
        
        if first_row_marked:
            for j in range(1, m):
                matrix[0][j]=0
        
        if first_col_marked:
            for i in range(0, n):
                matrix[i][0]=0
```