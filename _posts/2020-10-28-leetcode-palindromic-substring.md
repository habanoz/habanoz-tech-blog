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
- [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given a string, your task is to count how many palindromic substrings in this string.
> The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

### Example 1 
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

### Example 2
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

## Naive Solution

Starting from first index, find all substrings and do a palindrome check. 
No additional space is used thus space complexity is O(1). Time complexity is worse. For each starting char, there a N of them, all remaining chars (N-m) are used to form substrings. A palindrome check may have (N-m)/ comparisons. Which yields O(N^3) time complexity.    

```java
class Solution {
    public int countSubstrings(String s) {
        if(s.length()==0)return 0;
        if(s.length()==1)return 1;
        
        int count=s.length();
        char[] ca=s.toCharArray();
        for(int i=0;i<ca.length;i++){
            for(int j=i+1;j<ca.length;j++){
                if(isPalindrom(ca, i, j))
                    count+=1;    
            }
            
        }
        return count;
    }
    
    public boolean isPalindrom(char[] s,int start, int end){
        while(start<end){
            if(s[start]!=s[end])
                return false;
            start++;
            end--;
        }
        
        return true;
    }
}
```

## Expand Around Center Solution

A center is selected at each iteration. Substring is expanded around the center and for each substring a palindrome check is made.
Space complexity is again O(1). Time complexity analysis involves two loops. Outer loop moves the center 2N-1 times. In the inner loop substring is expanded and palindrome check is made which may involve N/2 O(1) operations. Time complexity is O(N^2).   

```java
class Solution {
    public int countSubstrings(String s) {
        if(s.length()==0)return 0;
        if(s.length()==1)return 1;
        
        char[] ca=s.toCharArray();
        int n = ca.length;
        
        int count=0;
        
        for(int center=0;center<2*n-1;center++){
            int left = center/2;
            int right = left + (center % 2);
            
            while (left>=0 && right<n && ca[left]==ca[right]) {
                left--;
                right++;
                count++;
            }
        }
        
        return count;
    }
}
```