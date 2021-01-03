---
title: "Leetcode: Jump Game"
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
- [Jump Game](https://leetcode.com/problems/jump-game/ "Go to leetcode"){:target="_blank" rel="noopener"}

>Given an array of non-negative integers nums, you are initially positioned at the first index of the array.

> Each element in the array represents your maximum jump length at that position.

> Determine if you are able to reach the last index.

### Example 1
```
Input: nums = [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

### Example 2
```
Input: nums = [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum jump length is 0, which makes it impossible to reach the last index.
```

## Solution

If the last element is reachable from any previous element then the question becomes if the previous element is reachable from any of its predecessors. 

canReach method takes three arguments. First one is obvious. Input array is not modified. Its last index is changed to act like it is a reduced array.
Second argument is the index of the first predecessor of the current last element.  
Third argument specifies how far are we from the last element. 

Space complexity is O(1) because no extra space is used. If stack space is counted, space complexity is O(N) because at worst case, canReach method is called N times.
Time complexity is O(N): At worst case canReach method is called N times. 

```python
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        if len(nums)==1:
            return True
        
        return self.canReach(nums, len(nums)-2, 0)
    
    def canReach(self, nums, n, b):
        N = len(nums)

        if n<0 or n<b:
            return False
        
        if nums[n-b]>=b+1:
            if n==0:
                return True
            else: return self.canReach(nums, n-1, 0)
        else:
            return self.canReach(nums, n, b+1)
```

