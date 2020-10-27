---
title: "Leetcode: Valid Numbers"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - Math
  - String
---

## Problem Description

Problem definition is taken from leetcode. 
- [Valid Numbers](https://leetcode.com/problems/valid-number/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Validate if a given string can be interpreted as a decimal number.

#### Examples:
```
"0" => true
" 0.1 " => true
"abc" => false
"1 a" => false
"2e10" => true
" -90e3   " => true
" 1e" => false
"e3" => false
" 6e-1" => true
" 99e2.5 " => false
"53.5e93" => true
" --6 " => false
"-+3" => false
"95a54e53" => false
```

## Solution


```java
class Solution {
    public boolean isNumber(String s) {
        final int ws=' ';
        final int n = s.length();
        
        if(n==0)return false;
            
        int pos=0;
        int end = s.length()-1;
        boolean exponent=false;
        
        while(pos<n && s.charAt(pos)==ws)pos++;
        while(end>pos && s.charAt(end)==ws)end--;
        String ss = s.substring(pos, end+1);
        
        if(ss.length()==0)return false;
        if(ss.charAt(0)=='e')return false;
        
        
        return isValidDecimal(ss, true, true, true, false);
    }
    
    public boolean isValidDecimal(String s, boolean expAllowed, boolean decimalAllowed, boolean signAllowed, boolean isEmptyAllowed){
        
        final int n = s.length();
        if(n==0) return isEmptyAllowed;
        
        int pos=0;
        boolean first=true;
        
        if(s.charAt(pos)=='-' || s.charAt(pos)=='+')
            if(signAllowed)
                return isValidDecimal(s.substring(pos+1), expAllowed, decimalAllowed, false, false);
        
        while(pos<n){
            char c = s.charAt(pos);
            
            if(c=='e')
                // "e1e"
                // ".e1"
                if(expAllowed && ( isEmptyAllowed || (!isEmptyAllowed && !first) ) )  return isValidDecimal(s.substring(pos+1), false, false, true, false);
                else return false;
            
            if(c=='.')
                // "."
                // ".3."
                // ".3"
                // "3."
                if(decimalAllowed) return isValidDecimal(s.substring(pos+1), expAllowed, false, false, !first);
                else return false;
            
            if(isNonDigit(c))
                return false;
            
            first = false;
            pos++;
        }
        return true;
    }
    
    public boolean isNonDigit(char c ){
        return c<'0' || c>'9';
    }
}
```

## Complexity Analysis

Time complexity is O(N) and space complexity is O(1). 
