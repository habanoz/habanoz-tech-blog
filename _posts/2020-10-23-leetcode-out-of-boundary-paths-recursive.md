---
title: "Leetcode: Out of Boundary Paths: Recursive Solution"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - recursion
  - memoization
  - depth-first-search
  - DFS
---

## Problem Description

Problem definition is taken from leetcode. 
- [Out of Boundary Paths](https://leetcode.com/problems/out-of-boundary-paths/ "Go to leetcode"){:target="_blank" rel="noopener"}

Dynamic programming solution is given at [Dynamic Programming Solution]({{ site.baseurl }}{% post_url 2020-10-23-leetcode-out-of-boundary-paths-dp %})

## Solution
Brute force recursive approach involves traversing all search space until all moves are completed and counting number of times ball is out off the board. A memo arrays of size Nxmxn is used to memorize already visited cell so that it is not calculated again. 

memo array cells are set 0 by default. It is not initialized again to save computing time. To differentiate unvisited cells from cells having 0 paths, -1 is used. If -1 is found, it is interpreted as 0. 

Each cell has four neighbour cells. At each cell, four recursivePathSum calls are made. Results are summed using a long variable. Mode of long variable is taken and set to an integer variable.   

Symmetric cells share the same number of paths. Result is set to 4 elements of the memo array. First element corresponds to current (N, i, j) value. 3 vales are symmetric cells. To save more space, it is possible to use a memo array of size Nx(m/2+1)x(n/2+1). In that case it would be necessary to translate actual i,j indices to symmetric indices found in the contracted memo array.

## Implementation

```java
class Solution {
    final int[] di={-1, 0, 1, 0}; // up, right, down, left
	final int[] dj={ 0, 1, 0,-1}; // up, right, down, left
	final int base = (int) Math.pow(10,9)+7;
	
	public int findPaths(int m, int n, int N, int i, int j) {
		int[][][] sums = new int[N][m][n];

		return recursivePathSum(m, n, N, i, j, sums);
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

		int sum = (int) (lsum %  base);

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

Memo array is Nxmxn thus space complexity is O(Nmn). 
Time complexity is O(Nxmxn) due to size of the memo array. Even though the memo array is not explicitly initialized, it is implicitly initialized with zeros.
