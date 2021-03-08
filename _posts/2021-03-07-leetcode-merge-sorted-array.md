---
title: "Leetcode: Merge Sorted Array"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
  - Two pointers
---

## Problem Description

Problem definition is taken from leetcode. 
- [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.
> The number of elements initialized in nums1 and nums2 are m and n respectively. You may assume that nums1 has a size equal to m + n such that it has enough space to hold additional elements from nums2.

### Example 1
```
Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
Output: [1,2,2,3,5,6]
```

### Example 2
```
Input: nums1 = [1], m = 1, nums2 = [], n = 0
Output: [1]
```


## Solution 1
Copy nums1 into another list named3. Merge nums2 and nums3 into nums1.

Space complexity is O(M). 
Time complexity is O(M+N).

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        nums3 = [nums1[i] for i in range(m)]

        i = 0
        j = 0
        k = 0
        
        while k < m and j < n:
            
            if nums3[k]<nums2[j]:
                nums1[i] = nums3[k]
                k = k+1
            else:
                nums1[i] = nums2[j]
                j = j+1
            
            i = i+1
        
        while k==m and j<n: 
            nums1[i] = nums2[j]
            j = j+1
            i = i+1
            
        while j==n and k<m: 
            nums1[i] = nums3[k]
            k = k+1
            i = i+1
```

## Solution 2

Inspired from a leetcode user post. Uses a backward approach that eliminates the need for an additional temporary array creation.

Space complexity is O(1).
Time complexity is O(M+N).

> https://leetcode.com/problems/merge-sorted-array/discuss/29522/This-is-my-AC-code-may-help-you

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        
        k = n+m-1
        i = m-1
        j = n-1
        
        while i>=0 and j>=0:
            if nums1[i]>nums2[j]:
                nums1[k] = nums1[i]
                i = i-1
            else:
                nums1[k] = nums2[j]
                j = j-1
            
            k = k-1
        
        while j>=0:
            nums1[k] = nums2[j]
            j = j-1
            k = k-1
```