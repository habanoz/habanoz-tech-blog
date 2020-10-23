---
title: "Leetcode: Knight Probability in Chessboard: Recursive Solution"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - dynamic programming
  - recursive solution
---

## Problem Description

Problem description is given in [problem description]({{ site.baseurl }}{% post_url 2020-10-22-leetcode-knight-probability-in-chessboard %}).

## Recursive Solution

At each position a knight may go to 8 new positions. Probability of moving to a new position is probability of being at current position divided by 8. Thus we can recursively calculate probabilities for each move. After last move, we can take sum of all probabilities which gives total probability of staying on board.  

The knight starts at row r and column c in a board of NxN. K shows total moves, k shows kth move. Probability of being on board at kth move is given by function f.

![\begin{align*}
f(r,c,k)= \sum_{(r_{prev}, c_{prev})\epsilon S} f(r_{prev}, c_{prev}, k-1) / 8
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5CLarge+%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0Af%28r%2Cc%2Ck%29%3D+%5Csum_%7B%28r_%7Bprev%7D%2C+c_%7Bprev%7D%29%5Cepsilon+S%7D+f%28r_%7Bprev%7D%2C+c_%7Bprev%7D%2C+k-1%29+%2F+8%0A%5Cend%7Balign%2A%7D%0A)

S contains all previous positions where the knight can move from to position (r,c).

At start where k=0;

![\begin{align*}
f(r,c,0)= 1
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Clarge+%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0Af%28r%2Cc%2C0%29%3D+1%0A%5Cend%7Balign%2A%7D%0A) 

## Implementation

For initial position probability is set to 1. Since older probabilities are not needed, only two arrays (dp and dpNext) are used to keep current and previous probabilities. After each move arrays are swapped. 

Next positions are calculated using dr and dc arrays. Obviously the arrays contain 8 elements which are used to calculate all possible 8 next positions. Off-board positions are ignored. 

After the final move, sum of all probabilities is returned.  

```java
class Solution {

    public double knightProbability(int N, int K, int r, int c) {
        return recursiveFindProbability(N, K, r,c);
    }
    
    public double recursiveFindProbability(int N, int K, int r, int c){
        double[][] dp = new double[N][N];
        
        int[] dr = new int[]{2, 2, 1, 1, -1, -1, -2, -2};
        int[] dc = new int[]{1, -1, 2, -2, 2, -2, 1, -1};
        
        dp[r][c] = 1.0;
        
        while(K-->0){
            double[][] dpNext = new double[N][N];
            for(int i=0;i<N;i++){
                for(int j=0;j<N;j++){
                    for(int m=0;m<8;m++){
                        int mi = i+dr[m];
                        int mj = j+dc[m];
                        if(areWeOnBoard(N, mi, mj)){
                            dpNext[mi][mj] += dp[i][j]/8; 
                        }
                    }
                }
            }
            
            dp = dpNext;
        }
        
        return sum(dp);
    }
    
    public double sum(double[][] arr){
        double sum=0.0;
        for(double arr1[] : arr)
            for(double a: arr1)
                sum+=a;
        
        return sum;
    }

    public boolean areWeOnBoard(int N, int r, int c){
        if(r<N && r>=0 && c<N && c>=0)
            return true;
        
        return false;
    }
}
```

## Complexity

Space complexity is ![O(N^2)](https://render.githubusercontent.com/render/math?math=%5Ctextstyle+O%28N%5E2%29). Time complexity is ![O(8xKxNxN)=O(N^2)](https://render.githubusercontent.com/render/math?math=%5Ctextstyle+O%288xKxNxN%29%3DO%28N%5E2%29). After each move, all probabilities are calculated using probabilities from 8 previous positions. 