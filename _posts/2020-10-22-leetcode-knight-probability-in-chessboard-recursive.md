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

Problem description is given in [Leetcode: Knight Probability in Chessboard]({{ site.baseurl }}{% post_url 2020-10-22-leetcode-knight-probability-in-chessboard %}).

## Recursive Solution

At each position a knight may go to 8 new positions. Probability of moving to a new position is probability of being at current position divided by 8. Thus we can recursively calculate probabilities for each move. After last move, we can take sum of all probabilities which gives total probability of staying on board.  

The knight starts at row r and column c in a board of NxN. K shows total moves, k shows kth move. Probability of being on board after k moves is given by function f.

![\begin{align*}
f(r,c,k)= \sum_{(r_{next}, c_{next})\epsilon S} f(r_{next}, c_{next}, k+1) / 8
\end{align*}](https://render.githubusercontent.com/render/math?math=%5CLarge+%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0Af%28r%2Cc%2Ck%29%3D+%5Csum_%7B%28r_%7Bnext%7D%2C+c_%7Bnext%7D%29%5Cepsilon+S%7D+f%28r_%7Bnext%7D%2C+c_%7Bnext%7D%2C+k%2B1%29+%2F+8%0A%5Cend%7Balign%2A%7D)

At the beginning k=0. S contains 8 next possible positions where the knight can move from current position.

At the end where k=K;

![\begin{align*}
f(r,c,K)= 1
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Clarge+%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0Af%28r%2Cc%2CK%29%3D+1%0A%5Cend%7Balign%2A%7D%0A) 

## Implementation

Recursive implementation calculates probabilities by making depth-first-search in the movements space. Each recursive function call makes 8 new calls and takes average of the results and returns the average result.  

There are 3 base cases. 
- The night is off-board.
- The night makes K moves and still in the board.
- Current cell is already visited and probability value is cached.

In recursive case:
- Makes 8 recursive calls for possible 8 new positions.
- Take average of all probabilities returned by recursive calls. Cache the resulting probability.
- Return the probability.

```java
class Solution {
    public double knightProbability(int N, int K, int r, int c) {
        double[][][] probs = new double[K+1][N][N];
        return recursiveFindProbability(N, K, r, c, probs);
    }
    
    public double recursiveFindProbability(int N, int K, int r, int c, double[][][] probs){
        boolean onBoard = areWeOnBoard(N, r, c);
        
        if(!onBoard)
            return 0;
        
        if(K==0)
            return 1.0;
        
        
        if(probs[K][r][c]>0){
            return probs[K][r][c];
        }
        
        int[] dr = new int[]{2, 2, 1, 1, -1, -1, -2, -2};
        int[] dc = new int[]{1, -1, 2, -2, 2, -2, 1, -1};
        
        double probSum=0;
        for (int m=0;m<8;m++){
            int nr = r+dr[m];
            int nc = c+dc[m];
            
            probSum +=recursiveFindProbability(N, K-1, nr, nc, probs);
        }
        
        probSum/=8;
        
        probs[K][r][c] = probSum;
        
        return probSum;
    }
    
    public boolean areWeOnBoard(int N, int r, int c){
        if(r<N && r>=0 && c<N && c>=0)
            return true;
        
        return false;
    }
}
```

## Complexity

Space complexity is ![O(KxN^2)](https://render.githubusercontent.com/render/math?math=%5Ctextstyle+O%28KxN%5E2%29). We need to keep probabilities for each cell after each move. 

Time complexity is ![O(8^K)](https://render.githubusercontent.com/render/math?math=%5Ctextstyle+O%288%5EK%29%0A). 

At each method execution, 8 more methods are called. Depth of the call tree is determined by K. 

![O(8^0)+O(8^1)+O(8^2)+...+O(8^K) = O(8^K)](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+O%288%5E0%29%2BO%288%5E1%29%2BO%288%5E2%29%2B...%2BO%288%5EK%29+%3D+O%288%5EK%29)
