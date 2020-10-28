---
title: "Leetcode: Longest Palindromic Substrings"
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
- [Longest Palindromic Substrings](https://leetcode.com/problems/longest-palindromic-substring/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a string s, return the longest palindromic substring in s.
  
### Example 1 
```
Input: s = "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

### Example 2
```
Input: s = "cbbd"
Output: "bb"
```

## Expand Around Center Solution

A center is selected at each iteration. Substring is expanded around the center and for each substring a palindrome check is made.
Space complexity is again O(1). Time complexity analysis involves two loops. Outer loop moves the center 2N-1 times.There can be 2N-1 centers: N centers (odd length palindromes) for each char positions and N-1 centers (even length palindromes) between two char positions. In the inner loop substring is expanded and palindrome check is made which may involve N/2 O(1) operations. Time complexity is O(N^2).   

Same approach can be used to solve the counting palindromic substrings problem in [Palindromic Substring]({{ site.baseurl }}{% post_url 2020-10-28-leetcode-palindromic-substring %})

```java
class Solution {
    
    public String longestPalindrome(String s) {
        if(s.length()==0 || s.length()==1)return s;
        
        char[] ca=s.toCharArray();
        int n = ca.length;
        
        int longest = 0;
        int start=0;
        int end=0;
        
        for(int center=0;center<2*n-1;center++){
            int left = center/2;
            int right = left + (center % 2);
            
            while (left>=0 && right<n && ca[left]==ca[right]) {
                if(right-left+1> longest){
                    
                    start=left;
                    end=right;
                    longest = right-left+1;
                }
                
                left--;
                right++;
            }
        }
        
        return new String(Arrays.copyOfRange(ca, start, end+1));
    }
}
```