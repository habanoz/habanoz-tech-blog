---
title: "Leetcode: Generate Parentheses"
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
- [Generate Parentheses](https://leetcode.com/problems/generate-parentheses/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

### Example 1 
```
Input: n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

### Example 2
```
Input: n = 1
Output: ["()"]
```

## Solution

Recursive backtracking method takes 3 inputs: current combination, left brackets available and right brackets available. 

Within bt method, if no left bracket is left, use all right brackets and return. Otherwise use a left bracket. If there are more right brackets available than left brackets use one right bracket.   

Complexity analysis is omitted. 
 
```java
class Solution {
    List<String> result = new ArrayList<>();
    
    public List<String> generateParenthesis(int n) {
        bt("", n, n);
        return result;
    }
    
    public void bt(String comb, int open, int close){
        if(open==0){
            while(close-->0) comb+=')';
            result.add(comb);
        } else {
            bt(comb+'(', open-1, close );
            if(open < close)
                bt(comb+')', open, close-1 );
        }
    }
}
```
