---
title: "Leetcode: Palindromic Substrings"
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
- [Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Write a function to find the longest common prefix string amongst an array of strings.

### Example 1 
```
Input: strs = ["flower","flow","flight"]
Output: "fl"
```

### Example 2
```
Input: strs = ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

## Iterative Prefix Search

Choose first string as base. Starting from first position, if all strings has the same chars, position is incremented. No additional space is used. Space complexity is O(1). n being number of strings, m being length of base string, time compexity is O(mn).

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        final int n = strs.length;
        if(n==0)return "";
        if(n==1)return strs[0];
        
        int pos = 0;
        String base=strs[0];
        
        while (pos<base.length()){
            char c = base.charAt(pos);
            
            for(int i=1;i<n;i++){
                if(strs[i].length()<=pos || strs[i].charAt(pos)!=c)
                    return base.substring(0, pos);
            }
            
            pos++;
        } 
        
        return base.substring(0, pos);

    }
}
```

