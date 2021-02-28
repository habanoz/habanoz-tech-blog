---
title: "Leetcode: Combinations"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Backtracking
---

## Problem Description

Problem definition is taken from leetcode. 
- [Combinations](https://leetcode.com/problems/combinations/ "Go to leetcode"){:target="_blank" rel="noopener"}

>Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.
>You may return the answer in any order.

### Example 1
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

### Example 2
```
Input: n = 1, k = 1
Output: [[1]]
```


## Solution 1

Recursively create combinations. Time complexity is O(n^k). Space complexity is O(k).

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        combinations = []
        
        self.populate(combinations, n, [], 0, k)
        
        return combinations
        
        
    def populate(self, combinations, N, comb, idx, k):
        if k==0: 
            combinations.append(comb)
            return
        
        for i in range(idx, N):
            self.populate(combinations, N, comb+[i+1], i+1, k-1)

```