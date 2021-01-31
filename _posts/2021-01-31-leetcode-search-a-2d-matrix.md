---
title: "Leetcode: Search a 2D Matrix"
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
- [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
> - Integers in each row are sorted from left to right.
> - The first integer of each row is greater than the last integer of the previous row.

### Example 1
![example1](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```

### Example 2
![example2](https://assets.leetcode.com/uploads/2020/10/05/mat2.jpg)
```
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```


## Solution 1

The solution is two-phased. In the first phase relevant row is found using binary search. 
In the second phase relevant column is found using binary search.  

Time and space complexity is O(logm+logn)=O(logmn). If recursion is converted to iteration, space complexity becomes O(1).

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        row = self.find_row(matrix, 0, len(matrix), target)
        return self.find_col(row, 0, len(row), target)>=0 if row else False
    
    def find_row(self, matrix, i0, i1, target):
        if i0>=i1: return None
        
        middle = (i1+i0)//2
        
        row = matrix[middle]
        
        if row[0]<= target and row[-1]>=target:
            return row
        elif row[0]> target:
            return self.find_row(matrix, i0, middle, target)
        else: 
            return self.find_row(matrix, middle+1, i1, target)
        
    def find_col(self, arr, j0, j1, target):
        if j0>=j1: return -1
        
        middle = (j0+j1)//2
        
        if arr[middle]==target:
            return middle 
        elif arr[middle]>target:
            return self.find_col(arr, j0, middle, target)
        else: return self.find_col(arr, middle+1, j1, target)     
```

# Solution 2

The whole matrix is treated as a single long list. Binary search is applied to the list. List index is converted to matrix indices.   

Time and space complexity is similar to the solution 1.

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        return self.find_col(matrix, 0, len(matrix)*len(matrix[0]), target)
        
    def find_col(self, matrix, j0, j1, target):
        if j0>=j1: return False
        
        middle = (j0+j1)//2
        mVal = matrix[middle//len(matrix[0])][middle%len(matrix[0])]
        
        if mVal==target:
            return True 
        elif mVal>target:
            return self.find_col(matrix, j0, middle, target)
        else: return self.find_col(matrix, middle+1, j1, target)
```