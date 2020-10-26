---
title: "Leetcode: Longest Substring Without Repeating Characters"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - Sliding window
  - Two pointers
  - String
---

## Problem Description

Problem definition is taken from leetcode. 
- [Out of Boundary Paths](https://leetcode.com/problems/longest-substring-without-repeating-characters/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a string s, find the length of the longest substring without repeating characters.

### Example 1 
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

### Example 2
```
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## Solution
A sliding window [i,j] is used to keep substrings which having unique chars. A char array ca is used to store the index value (ci) where a char is found.
At each iteration j is incremented. If the next char in the string is already present withing the sliding window at index ci, start index (i) is set to ci+1.

## Implementation

```java
class Solution {
    static final int MAX_CHARS=128;
    
    public int lengthOfLongestSubstring(String s) {
        
        if(s.length()<2)
            return s.length();
        
        int longest=1;
        int start=0;
        int end=start+1;
        
        int[] ca=new int[MAX_CHARS]; 
        Arrays.fill(ca, -1);
        ca[s.charAt(0)]=start;
        
        while(end<s.length()){
            char c = s.charAt(end);
            int ci = ca[c];
            
            if(ci<start)
                longest=Math.max(longest, end-start+1);           
            else 
                start=ci+1;   
            ca[c]=end++;
        }   
        return longest;
    }
}
```

## Complexity

Space complexity is O(m) where m is the number of elements in the set of chars the input string may contain. 
Time complexity is O(n) where n is the length of the input string. Each position in the input string is visited once.  

