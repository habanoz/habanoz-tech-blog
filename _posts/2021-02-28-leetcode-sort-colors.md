---
title: "Leetcode: Sort Colors"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
  - Two Pointers
  - Sort
---

## Problem Description

Problem definition is taken from leetcode. 
- [Sort Colors](https://leetcode.com/problems/sort-colors/ "Go to leetcode"){:target="_blank" rel="noopener"}

>Given an array nums with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.
>We will use the integers 0, 1, and 2 to represent the color red, white, and blue, respectively.

### Example 1
```
Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2] 
```

### Example 2
```
Input: nums = [2,0,1]
Output: [0,1,2]
```


## Solution 1

Keep two indices, idx_left and idx_right. Left of idx_left should contain 0s, right of idx_right should contain 2s.

Time complexity is O(N) and space complexity is O(1).

```python
class Solution:
    def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """        
        idx_left=0
        idx_right=len(nums)-1
        while idx_left<len(nums) and nums[idx_left]==0: idx_left+=1
        while idx_right>=0 and nums[idx_right]==2: idx_right-=1
            
        idx=idx_left
        
        while idx<len(nums) and idx<=idx_right:
            val = nums[idx]
            
            if val==0:
                self.swap(nums, idx_left, idx)
                while idx_left<len(nums) and nums[idx_left]==0: idx_left+=1
            elif val==2:
                self.swap(nums, idx_right, idx)
                while idx_right>=0 and nums[idx_right]==2: idx_right-=1
            
            if nums[idx]!=0 or idx<=idx_left:
                idx+=1
        
    
    def swap(self, nums, i1, i2):
        if i1==i2:
            return
        
        temp = nums[i1]
        nums[i1]=nums[i2]
        nums[i2]=temp 
```