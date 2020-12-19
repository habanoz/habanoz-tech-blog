---
title: "Leetcode: Group Anagrams"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - String
---

## Problem Description

Problem definition is taken from leetcode. 
- [Group Anagrams](https://leetcode.com/problems/group-anagrams/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given an array of strings strs, group the anagrams together. You can return the answer in any order.

> An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

### Example 1 
```
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

### Example 2
```
Input: strs = [""]
Output: [[""]]
```

## Solution

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        
        d = dict()
        
        for s in strs:
            sorted_string = ''.join(sorted(s))
            
            if sorted_string not in d:
                d[sorted_string]=list()
            
            d.get(sorted_string).append(s)
        
        return [d[k] for k in d]
        
```

