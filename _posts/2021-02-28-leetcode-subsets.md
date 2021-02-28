---
title: "Leetcode: Subsets"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
  - Backtracking
---

## Problem Description

Problem definition is taken from leetcode. 
- [Subsets](https://leetcode.com/problems/subsets/ "Go to leetcode"){:target="_blank" rel="noopener"}

>Given an integer array nums of unique elements, return all possible subsets (the power set).
>The solution set must not contain duplicate subsets. Return the solution in any order.

### Example 1
```
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

### Example 2
```
Input: nums = [0]
Output: [[],[0]]
```


## Solution 1

Populate subsets by adding current combination to combination list at each step.

Time complexity is O(N) and space complexity is O(N).

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        subs = []
        
        self.populate(subs, nums, [], 0)
        
        return subs
        
    def populate(self, subsc, nums, comb, idx):
        subsc.append(comb)
        
        if idx==len(nums):
            return
        
        for i in range(idx, len(nums)):
            self.populate(subsc, nums, comb+[nums[i]], i+1 )
        
```