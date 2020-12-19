---
title: "Leetcode: Pow(x, n)"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Math
  - Binary Search
  - Divide And Conquer
---

## Problem Description

Problem definition is taken from leetcode. 
- [Pow(x, n)](https://leetcode.com/problems/powx-n/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Implement pow(x, n), which calculates x raised to the power n (i.e. xn).

### Example 1 
```
Input: x = 2.00000, n = 10
Output: 1024.00000
```

### Example 2
```
Input: x = 2.10000, n = 3
Output: 9.26100
```

## Solution

```python
class Solution:
    d = None
    def myPow(self, x: float, n: int) -> float:
        if n==1 : return x
        if n==0 : return 1
        
        self.d = dict()
        
        if n<0 : x = 1/x 
        n = abs(n)
        
        return self.divideConquer(x, n)
    
    def divideConquer(self, x, n):
        if n==1:
            return x
        elif n==2:
            return x*x
        elif n==3:
            return x*x*x
        
        if n in self.d:
            return self.d[n]
        
        res =  self.divideConquer(x, math.ceil(n/2))* self.divideConquer(x, math.floor(n/2))
        
        self.d[n]=res
        
        return res
        
```

