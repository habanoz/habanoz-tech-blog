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

![formula](https://render.githubusercontent.com/render/math?math=\LARGE&space;f(r,c,k)=&space;\sum_{(r_{prev},&space;c_{prev})\epsilon&space;S}&space;f(r_{prev},&space;c_{prev},&space;k-1)&space;/&space;8)





