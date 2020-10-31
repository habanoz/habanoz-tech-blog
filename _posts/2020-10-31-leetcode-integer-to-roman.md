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
- [Integer to Roman](https://leetcode.com/problems/integer-to-roman/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M. Given an integer, convert it to a roman numeral.
> 1 <= num <= 3999

### Example 1 
```
Input: num = 3
Output: "III"
```

### Example 2
```
Input: num = 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.s
```

## Solution

Roman symbols and values are kept in arrays. Derived symbols and their values are also kept in the map in the correct position. Right most element in the arrays has the greatest value. Left most element in the arrays has the smallest value. Symbols are iterated from right to left effectively from biggest to smallest. If a symbol value is greater than or equal to the number it means the number contains the symbol. After each match, symbol value is subtracted from the number until the number reaches zero or all symbols are iterated.   

If num==3338 it probably has the longest roman numeral form. 3338 in roman numeral form has the value "MMMCCCXXXVIII" which has 13 roman symbols thus iterates 13 times. At worst case the algorithm will make 13 iterations and 13 digits will be stored in StringBuilder. It is fair to say space and time complexity is O(1). 

```java
class Solution {
    public String intToRoman(int num) {
        int[]  values =  new int[]{ 1, 4, 5, 9, 10, 40, 50, 90, 100, 400, 500, 900, 1000};
        String[] symbols = new String[]{"I","IV","V","IX","X","XL","L","XC","C","CD","D","CM", "M"};
        
        StringBuilder builder=new StringBuilder();
        
        for (int i=values.length-1;num>0 && i>=0;i--){
            int value=values[i];
            String symbol=symbols[i];

            while(num>=value){
                num-=value;
                builder.append(symbol);
            }
        }
        return builder.toString();
    }
}
```

