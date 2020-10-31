---
title: "Leetcode: Letter Combinations of a Phone Number"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - String
  - Backtracking
---

## Problem Description

Problem definition is taken from leetcode. 
- [Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent. Return the answer in any order.

### Example 1 
```
Input: digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

### Example 2
```
Input: digits = "2"
Output: ["a","b","c"]
```

## Solution

An array stores list of chars that corresponds to a digit. A hash map can also be used. 

Starting from the first digit, for each character mapped by the digit a new StringBuilder is created and added to builders list. 

Assume first digit maps to m chars and second digit maps to n chars. After first digit is processed there will be m builders in builders list. After second digit is processed there will be m*n builders. m*n-m builders is created by copying m builders already created in the previous iteration.       

Most digits maps to three characters. Number of digits in the input string is d. Time complexity is O(d*3^d). builder list may have 3^d builders each having d characters.
Time complexity is O(3*d*3^d)=O(d*d^3). For each digit, all builders are appended 3 new chars. Number of builders increase at each iteration, there are at most d^3 builders.    

```java
class Solution {
    static final List[] mappings=new List[]{
        Arrays.asList('a','b','c'), 
        Arrays.asList('d','e','f'), 
        Arrays.asList('g','h','i'), 
        Arrays.asList('j','k','l'), 
        Arrays.asList('m','n','o'), 
        Arrays.asList('p','q','r','s'), 
        Arrays.asList('t','u','v'), 
        Arrays.asList('w','x','y','z')
    };
    
    public List<String> letterCombinations(String digits) {
        if(digits.length()==0)return Collections.emptyList();
        
        List<StringBuilder> builders = new ArrayList<>();
        
        List<Character> firstDigitChars = mappings[digits.charAt(0)-'2'];
        for(int c=0;c<firstDigitChars.size();c++){
            builders.add(new StringBuilder(Character.toString(firstDigitChars.get(c))));
        }
        
        for (int d=1;d<digits.length();d++){
            List<Character> chars=mappings[digits.charAt(d)-'2'];

            int nb=builders.size();
            for (int b=0;b<nb;b++) {
                StringBuilder builderB = builders.get(b);
                for(int c=1;c<chars.size();c++){  
                    builders.add(new StringBuilder(builderB).append(chars.get(c)));
                }
                builderB.append(chars.get(0));
            }       
        }
        
        return builders.stream().map(b->b.toString()).collect(Collectors.toList());
    }
}
```

