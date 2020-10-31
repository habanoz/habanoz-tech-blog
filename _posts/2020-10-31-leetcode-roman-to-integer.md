---
title: "Leetcode: Palindromic Substrings"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - String
  - Math
---

## Problem Description

Problem definition is taken from leetcode. 
- [Roman to Integer](https://leetcode.com/problems/roman-to-integer/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M. Given a roman numeral, convert it to an integer.

### Example 1 
```
Input: s = "III"
Output: 3
```

### Example 2
```
Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## Solution

Roman symbols and values are kep inside a map. Normally a roman numeral contains smallest symbol at the left most position. Biggest symbol is at right most position. If a symbol is smaller then its right position, then it needs to be subtracted from the sum. Otherwise, symbol value is added to the sum. 
Space complexity is O(1). The map uses extra space which is O(1), but it is defined as static so it is initialized once for all test cases.  Time complexity is O(N), N being the length of the roman numeral.
```java
class Solution {
    static final Map<Character,Integer> map = new HashMap<>();
    static{ 
        map.put('I',1);
        map.put('V',5);
        map.put('X',10);
        map.put('L',50);
        map.put('C',100);
        map.put('D',500);
        map.put('M',1000);
    }
    
    public int romanToInt(String s) {

        final int n = s.length();
        final char[] ca = s.toCharArray();
        
        int num=0;
        int lastVal=-1;
        
        for(int si=n-1;si>=0;si--){
            char cc=ca[si];
            int cval = map.get(cc);
            
            if(cval<lastVal){
                num-=cval;
            } else {
                num+=cval;
                lastVal = cval;
            }

        }
        return num;
    }
}
```

