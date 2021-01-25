---
title: "Leetcode: Plus One"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Math
  - String
---

## Problem Description

Problem definition is taken from leetcode. 
- [Add Binary](https://leetcode.com/problems/add-binary/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given two binary strings a and b, return their sum as a binary string.

### Example 1
```
Input: a = "11", b = "1"
Output: "100"
```

### Example 2
```
Input: a = "1010", b = "1011"
Output: "10101"
```

## Solution - Zip Function

itertools.zip_longest is used to zip uneven lists. Note that lists are reversed to start adding from the right most digit. 

At the end result is reversed back to normal order.

Space and time complexity is O(N), N being the greatest one of len(a) and len(b).

```python
import itertools

class Solution:
    def addBinary(self, a: str, b: str) -> str:
        carry=0
        result=[]
        
        for d1,d2 in itertools.zip_longest(reversed(list(a)),reversed(list(b))):
            d = int(d1 or 0)+int(d2 or 0)+carry
               
            carry = d // 2
            d = d % 2
            
            result.append(d)
            
        if carry:
            result.append(carry)
            
        return ''.join([str(c) for c in reversed(result)])
```

# Solution - Pop Function

Pop function can be used to reverse iterate over list elements.

Space and time complexity is O(N), N being the greatest one of len(a) and len(b).

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        l1 = list(a)
        l2 = list(b)
        carry = 0
        result = ''
        
        while l1 or l2 or carry:
            val = int(l1.pop() if l1 else 0)+int(l2.pop() if l2 else 0)+carry
            result += str(val%2)
            carry = val // 2
        
        return result[::-1]
```

# Solution - Recursive

Recursive solution uses last element indexing to traverse string elements in reverse order.
No actual addition is done. Instead, if digits are not similar then there is no carry, appending '1' is enough.
If digits are the same and equals to '0' then there is no carry and appending '0' is enough.
Otherwise, digits are equal to '1', in this case carry is needed, carry is applied as an additional call.

Time complexity analysis needed!!!

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        if not a :return b
        if not b :return a
        
        if a[-1] == b[-1]:
            if a[-1] == '1':
                return self.addBinary(self.addBinary(a[:-1],b[:-1]),'1')+'0'
            else: 
                return self.addBinary(a[:-1],b[:-1])+'0'
        
        return self.addBinary(a[:-1],b[:-1])+'1'
```

