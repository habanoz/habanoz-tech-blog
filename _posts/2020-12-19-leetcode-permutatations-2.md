---
title: "Leetcode: Permutations II"
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
- [Permutations 2](https://leetcode.com/problems/permutations-ii/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

### Example 1 
```
Input: nums = [1,1,2]
Output:
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

### Example 2
```
Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

## Recursive Solution

Solution is similar to [Permutations 1]({{ site.baseurl }}{% post_url 2020-12-19-leetcode-permutatations %}) where duplicate numbers are not allowed. Duplicate numbers are not used when generating new permutations but passed to next permutation.

```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        
        results=[]
        self.permuteRec(results, nums, [])
        return results
    
    def permuteRec(self, results, nums, perm):
        unums = list(set(nums))
        
        if nums:
            for idx in range(len(unums)):
                n = unums[idx]
                new_nums = list(nums)
                new_nums.remove(n)
                
                self.permuteRec(results, new_nums, perm+[n])
        else:
            results.append(perm)
```

