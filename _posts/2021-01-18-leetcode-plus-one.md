---
title: "Leetcode: Plus One"
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
- [Plus One](https://leetcode.com/problems/plus-one/ "Go to leetcode"){:target="_blank" rel="noopener"}

>Given a non-empty array of decimal digits representing a non-negative integer, increment one to the integer.

>The digits are stored such that the most significant digit is at the head of the list, and each element in the array contains a single digit.

>You may assume the integer does not contain any leading zero, except the number 0 itself.

### Example 1
```
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
```

### Example 2
```
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```

## Solution

Space and time complexity is O(N)

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        result = []
        carry = 0
        increment = 1
        for d in reversed(digits):
            d = d+carry+increment
            carry = 0
            increment = 0
            
            if d >= 10:
                carry = 1
                d = d - 10
            
            result.append(d)
        
        if carry == 1:
            result.append(1)
        
        return reversed(result)
```

