---
title: "Leetcode: Gray Code"
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
- [Gray Code](https://leetcode.com/problems/gray-code "Go to leetcode"){:target="_blank" rel="noopener"}

> The gray code is a binary numeral system where two successive values differ in only one bit.
> Given an integer n representing the total number of bits in the code, return any sequence of gray code.
> A gray code sequence must begin with 0.


### Example 1
```
Input: n = 2
Output: [0,1,3,2]
Explanation:
00 - 0
01 - 1
11 - 3
10 - 2
[0,2,3,1] is also a valid gray code sequence.
00 - 0
10 - 2
11 - 3
01 - 1
```

### Example 2
```
Input: n = 1
Output: [0,1]
```


## Solution 1
for n=2 result is 00,10,11,01.
for n=3 result is:
00|0
00|1
10|1
10|0
11|0
11|1
01|1
01|0

Result for n can be calculated using result for n-1. For each element in n-1, number is flipped to left two times and adding the negated bit.   

Time and space complexity is O(n).

```python
class Solution:
    def grayCode(self, n: int) -> List[int]:
        if n == 1:
            return [0,1]
        if n == 2:
            return [0,1,3,2]
        
        codes = self.grayCode(n-1)
        new_codes = []
        bit = 0
        for code in codes:
            new_codes.append((code<<1)+bit)
            bit = 0 if bit == 1 else 1
            new_codes.append((code<<1)+bit)
            
        return new_codes
```
