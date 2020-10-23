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

## Solution

## Implementation


```java
class Solution {
    final int[] di={-1, 0, 1, 0}; // up, right, down, left
	final int[] dj={ 0, 1, 0,-1}; // up, right, down, left
	final long base = (long)Math.pow(10,9)+7;
	
	public int findPaths(int m, int n, int N, int i, int j) {
		int[][][] sums = new int[N][m][n];

		int sum = recursivePathSum(m, n, N, i, j, sums);

		return sum;
	}

	public int recursivePathSum(int m, int n, int N, int i, int j, int[][][] sums){
		if(isOffBoard(m,n,i,j))
			return 1;

		if(N==0)
			return 0;

		if(sums[N-1][i][j]>0)
			return sums[N-1][i][j];

		if(sums[N-1][i][j]<0)
			return 0;

		long lsum=0;
		for(int p=0;p<4;p++){
			int ni=i+di[p];
			int nj=j+dj[p];
			lsum+=recursivePathSum(m, n, N-1, ni, nj, sums);
		}

		int sum = (int)Math.floorMod(lsum, base);

		int translatedSum = sum;
		if(translatedSum==0)
			translatedSum = -1;

		sums[N-1][i][j]=translatedSum;
		sums[N-1][m-1-i][j]=translatedSum;
		sums[N-1][i][n-1-j]=translatedSum;
		sums[N-1][m-1-i][n-1-j]=translatedSum;

		return sum;
	}

	public boolean isOffBoard(int m, int n, int i, int j){
		return (i<0 || j < 0 || i >= m || j >= n);
	}
}
```

## Complexity
