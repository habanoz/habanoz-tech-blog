---
title: "Leetcode: Count and Say"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - String
---

## Problem Description

Problem definition is taken from leetcode. 
- [Count and Say](https://leetcode.com/problems/count-and-say/ "Go to leetcode"){:target="_blank" rel="noopener"}

> The count-and-say sequence is a sequence of digit strings defined by the recursive formula:
> * countAndSay(1) = "1"
> * countAndSay(n) is the way you would "say" the digit string from countAndSay(n-1), which is then converted into a different digit string.
>
> To determine how you "say" a digit string, split it into the minimal number of groups so that each group is a contiguous section all of the same character. Then for each group, say the number of characters, then say the character. To convert the saying into a digit string, replace the counts with a number and concatenate every saying.
> 

### Example 1 
```
Input: n = 4
Output: "1211"
Explanation:
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
```

## Solution

Function that decodes number to desired string form is defined with following recursion:

f(n) = decode(f(n-1)) 

Base step is n=1. Decode function takes output of f(n-1) and converts to the desired form.

Time complexity is O(2^n). countAndSay method is called n times. Each method call iterates over output of countAndSay(n-1) length of which is unpredictable. Assume countAndSay output length doubles each time. Total number of iterations is 1 + 2^1 + 2^2 + ... + 2^n.
Space complexity is O(2^n). countAndSay method is called n times. Each method call uses output of countAndSay(n-1) length of which is unpredictable. Assume countAndSay output length doubles each time. Total space used is 1 + 2^1 + 2^2 + ... + 2^n.

```java
class Solution {
    public String countAndSay(int n) {
        if(n-1==0)return "1";
        
        char[] previousString=countAndSay(n-1).toCharArray();
        
        StringBuilder nextStringBuilder = new StringBuilder();
        int charCounter=1;
        char lastChar=previousString[0];
        
        for(int i=1;i<previousString.length;i++){
            char currentChar=previousString[i];
            
            if(currentChar==lastChar)
                charCounter++;
            else {
                nextStringBuilder.append(charCounter).append(lastChar);
                charCounter=1;
                lastChar=currentChar;
            }
        }
        
        nextStringBuilder.append(charCounter).append(lastChar);
        
        return nextStringBuilder.toString();
    }
}
```
