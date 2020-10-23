---
title: "Leetcode: Knight Probability in Chessboard: Iterative Solution"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - dynamic programming
  - iterative solution
---

## Iterative Solution

At each position a knight may go to 8 new positions. Probability of moving to a new position is probability of being at current position divided by 8. Thus we can iteratively calculate probabilities for each move. After last move, we can take sum of all probabilities which gives total probability of staying on board.  

The knight starts at row r and column c in a board of NxN. K shows total moves, k shows kth move. Probability of being on board at kth move is given by function f.

![\begin{align*}
f(r,c,k)= \sum_{(r_{prev}, c_{prev})\epsilon S} f(r_{prev}, c_{prev}, k-1) / 8
\end{align*}
](https://render.githubusercontent.com/render/math?math=%5Cdisplaystyle+%5Cbegin%7Balign%2A%7D%0Af%28r%2Cc%2Ck%29%3D+%5Csum_%7B%28r_%7Bprev%7D%2C+c_%7Bprev%7D%29%5Cepsilon+S%7D+f%28r_%7Bprev%7D%2C+c_%7Bprev%7D%2C+k-1%29+%2F+8%0A%5Cend%7Balign%2A%7D%0A)



