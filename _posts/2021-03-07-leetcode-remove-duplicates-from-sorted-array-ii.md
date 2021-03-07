---
title: "Leetcode: Remove Duplicates from Sorted Array II"
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
- [Subsets](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.
> Do not allocate extra space for another array; you must do this by modifying the input array in-place with O(1) extra memory.

### Example 1
```
Input: nums = [1,1,1,2,2,3]
Output: 5, nums = [1,1,2,2,3]
Explanation: Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively. It doesn't matter what you leave beyond the returned length.
```

### Example 2
```
Input: nums = [0,0,1,1,1,1,2,3,3]
Output: 7, nums = [0,0,1,1,2,3,3]
Explanation: Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively. It doesn't matter what values are set beyond the returned length.
```


## Solution 1
if occurrence of the last number is beyond 2, copy next element respecting the gap value.

Time complexity is O(N) and space complexity is O(1).

```python
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        i = 1
        last_num = nums[0]
        occur = 1
        length = len(nums)
        gap = 0
        
        while i < length:
            nums[i] = nums[i+gap]
            val = nums[i]
            
            if val == last_num:
                occur = occur + 1
            else:
                last_num = val
                occur = 1
                
            if occur > 2:
                gap = gap + 1
                length = length - 1
            else:
                i = i+1
                
        return length
```

## Solution 2

Similar approach but more concise, taken from a leetcode user post.

https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/discuss/27987/Short-and-Simple-Java-solution-(easy-to-understand)

```java
class Solution{
  public int removeDuplicates(int[] nums) {
    int i = 0;
    for (int n : nums)
      if (i < 2 || n > nums[i - 2])
        nums[i++] = n;
    return i;
  }	
}
```