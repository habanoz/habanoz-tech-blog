---
title: "Leetcode: Out of Boundary Paths"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - dynamic programming
  - depth-first-search
  - DFS
---

## Problem Description

Problem definition is taken from leetcode. 
- [Out of Boundary Paths](https://leetcode.com/problems/out-of-boundary-paths/ "Go to leetcode"){:target="_blank" rel="noopener"}

Recursive solution is given at [Recursive Solution]({{ site.baseurl }}{% post_url 2020-10-23-leetcode-out-of-boundary-paths-recursive %})

## Solution

If a position is reachable at c moves, then neighbour positions can be reached in c+1 moves. If we keep an (mxn) array where each cell at step c contains number of paths ending in the cell, we can calculate number of paths the neighbour cells have at step c+1. 

Two such mxn arrays is used. dp keeps number of paths for each cell at step c. dpNext keeps number of paths for each cell at step c+1. After dpNext is filled, dp and dpNext is swapped and dpNext is reset.

## Implementation

```java
class Solution {
	final int base = (int) Math.pow(10,9)+7;
	    
    public int findPaths(int m, int n, int N, int i, int j) {
		return findPathsDp(m, n, N, i, j);
	}
    
    public int findPathsDp(int m, int n, int N, int i, int j){
        int[][] dp = new int[m][n];
        
        dp[i][j]=1;
        int c=1;
        int count=0;
        while(c++<=N){
            int[][] dpNext = new int[m][n];
            for(int ic=0;ic<m;ic++){
                for(int jc=0;jc<n;jc++){
                    
                    if(ic==0){
                        count+=dp[ic][jc];
                        count = count % base;
                    }
                    
                    if(jc==0){
                        count+=dp[ic][jc];
                        count = count % base;
                    }
                    
                    if(ic==m-1){
                        count+=dp[ic][jc];
                        count = count % base;
                    }
                    
                    if(jc==n-1){
                        count+=dp[ic][jc];
                        count = count % base;
                    }
                    
                    if(ic>0){
                        dpNext[ic][jc]+=dp[ic-1][jc];
                        dpNext[ic][jc]=dpNext[ic][jc] % base;
                    }
                    
                    if(jc>0){
                        dpNext[ic][jc]+=dp[ic][jc-1];
                        dpNext[ic][jc]=dpNext[ic][jc] % base;
                    }
                    
                    if(ic<m-1){
                        dpNext[ic][jc]+=dp[ic+1][jc];
                        dpNext[ic][jc]=dpNext[ic][jc] % base;
                    }
                    
                    if(jc<n-1){
                        dpNext[ic][jc]+=dp[ic][jc+1];
                        dpNext[ic][jc]=dpNext[ic][jc] % base;    
                    }
                    
                }
            }
            
            dp=dpNext;
        }
        
        return count;
    }
}
```

## Complexity

dp array is mxn thus space complexity is O(mn). 
Time complexity is O(Nxmxn). dp array is filled N times. 
