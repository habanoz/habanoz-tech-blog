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

## Iterative Solution

An array stores list of chars that corresponds to a digit. A hash map can also be used. 

Starting from the first digit, for each character mapped by the digit a new StringBuilder is created and added to builders list. 

Assume first digit maps to m chars and second digit maps to n chars. After first digit is processed there will be m builders in builders list. After second digit is processed there will be m*n builders. m*n-m builders is created by copying m builders already created in the previous iteration.       

Number of digits in the input string is d and assume all digits are mapped to 3 chars. Space complexity is O(dx3^d). builder list may have 3^d builders each having d characters.
Time complexity is O(3xdx3^d)=O(dx3^d). For each digit, all builders are appended 3 new chars. Number of builders increase at each iteration, there are at most d^3 builders.    

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


## Backtracking Solution

bt function takes input string and current position. For each char mapped to the digit in the current position btUtil is called. btUtil appends the char to the builder it is provided. If there is not more digits in the input string, btUtil terminates by adding final string to result list. If there are more digits, bt mathod is called with the position incremented.  
bt function creates a copy of each builder before passing to btUtil method. Original builder is used for the first char. This way number of builders created is optimized.

Number of digits in the input string is d and assume all digits are mapped to 3 chars. Space complexity is O(dx3^d). result list may have 3^d builders each having d characters.
Time complexity is O(3^d). btUtil is called 1+3+3^2+...+3^d times.     


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
        
        int n =digits.length();
        int capacity = (int) Math.pow(4, n);
        List<String> result = new ArrayList<>(capacity);
        
        bt(digits, 0, new StringBuilder(), result);
        
        return result;
    }
    
    public void bt(String digits, int pos, StringBuilder builder, List<String> result) {
        List<Character> chars=mappings[digits.charAt(pos)-'2'];
        
        for (int i=1;i<chars.size(); i++)
            btUtil(digits, pos, new StringBuilder(builder), result, chars.get(i));
        
        btUtil(digits, pos, builder, result, chars.get(0));        
    }
    
    public void btUtil(String digits, int pos, StringBuilder builder, List<String> result, char c){
        builder.append(c);
    
        if (pos<digits.length()-1)
            bt(digits, pos+1, builder, result);
        else 
            result.add(builder.toString());
    }
}
```

## Backtracking Solution 2

This solution is similar to the previous solution. However, this solution is slower due to string copy operations and easier to read and understand.  

Instead of using builders, current combination is passed to bt command. Instead of using position input substring is passed to bt command. 

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
        
        int n =digits.length();
        int capacity = (int) Math.pow(4, n);
        List<String> result = new ArrayList<>(capacity);
        
        bt(digits, "", result);
        
        return result;
    }
    
    public void bt(String input, String combination, List<String> result) {
        if(input.isEmpty()){
            result.add(combination);
            return;  
        }
        
        List<Character> chars=mappings[input.charAt(0)-'2'];
        
        for(Character c: chars)
            bt(input.substring(1), combination+c, result);
    }
}
```