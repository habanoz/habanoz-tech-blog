---
title: "Leetcode: Divide Two Integers"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - Math
---

## Problem Description

Problem definition is taken from leetcode. 
- [Divide Two Integers](https://leetcode.com/problems/divide-two-integers/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given two integers dividend and divisor, divide two integers without using multiplication, division, and mod operator.
  
>  Return the quotient after dividing dividend by divisor.
  
>  The integer division should truncate toward zero, which means losing its fractional part. For example, truncate(8.345) = 8 and truncate(-2.7335) = -2.

>  Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For this problem, assume that your function returns 231 − 1 when the division result overflows.

### Example 1 
```
Input: dividend = 10, divisor = 3
Output: 3
Explanation: 10/3 = truncate(3.33333..) = 3.
```

### Example 2
```
Input: dividend = 7, divisor = -3
Output: -2
Explanation: 7/-3 = truncate(-2.33333..) = -2.
```

## Solution

The environment allows integer that can only store values in the range [−2^31,  2^31 − 1].  Obviously, negative value range is wider. It might be good idea to do calculations in negative value domain. Sing of the output is stored in a variable and all inputs are converted to negative value range. 

Before returning the result, "fixed" method is used to correct the result sign.  

The algorithm first finds greatest multiple of the divisor that can divide the dividend. Note that a positive multiple of the divisor indicates overflow. 

```java
class Solution {
    int INTEGER_MIN_VALUE=(int)-Math.pow(2, 31);
    int INTEGER_MAX_VALUE=(int)(Math.pow(2, 31)-1);
    
    public int divide(int dividend, int divisor) {
        
        boolean negative=dividend<0^divisor<0;
        
        if(dividend == 0)return 0;
        
        if(dividend > 0)
            dividend=-dividend;
        
        if(divisor > 0)
            divisor=-divisor;
        
        if(divisor == -1)
            return fixed(dividend, negative);
        
        if(divisor < dividend)
            return 0;
        
        if(divisor == dividend)
            return fixed(-1, negative);
        
        int quotient=0;
        
        int n = 0;
        while (dividend <= divisor<<n+1 && 0 > divisor<<n+1) n++;
        
        for(int i=n;i>=0;i--){
            int iDivisor = divisor<<i;
            
            while(iDivisor >= dividend){
                dividend -= iDivisor;
                quotient -= (int)Math.pow(2, i);
            }
            
        }
      
        return fixed(quotient, negative);
    }
    
    public int fixed(int negativeResult, boolean negative){    
        if(negative)
            return negativeResult;
        
        if(negativeResult==INTEGER_MIN_VALUE)
            return INTEGER_MAX_VALUE;
        
        return -negativeResult;
    }
}
```
