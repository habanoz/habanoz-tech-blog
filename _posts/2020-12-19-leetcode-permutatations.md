---
title: "Leetcode: Permutations"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - backtracking
---

## Problem Description

Problem definition is taken from leetcode. 
- [Permutations](https://leetcode.com/problems/permutations/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

### Example 1 
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

### Example 2
```
Input: nums = [0,1]
Output: [[0,1],[1,0]]
```

## Iterative Solution

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        return self.permuteSeq(nums)
    
    def permuteSeq(self, nums):
        perms=[[]]
        
        for n in nums:
            new_perms = []
            for perm in perms:
                for i in range(len(perm)+1):
                    new_perms.append(perm[:i]+[n]+perm[i:])
            perms = new_perms
        return perms
```

## Recursive Solution

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        results=[]
        self.permuteRec(results, nums, [])
        return results
    
    def permuteRec(self, results, nums, perm):
        if nums:
            for idx in range(len(nums)):
                self.permuteRec(results, nums[:idx]+nums[idx+1:], perm+[nums[idx]])
        else:
            results.append(perm)
```
