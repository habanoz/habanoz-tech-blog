---
title: "Leetcode: Maximum Subarray"
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
- [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

> Follow up: If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

### Example 1 
```
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

### Example 2
```
Input: nums = [1]
Output: 1
```

## Solution

If the previous item is positive then sum with the current element. For next elements sum is accumulated. At the end find maximum element.
If all elements are negative, then returns single greatest element. 

Time complexity is O(N): list is traversed twice. 
Space complexity is O(1): no extra space is used.

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for i in range(1, len(nums)):
            if nums[i-1] > 0:
                nums[i] += nums[i-1]
        return max(nums)

```

