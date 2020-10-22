---
title: "Leetcode: Knight Probability in Chessboard"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - dynamic programming
---

## Problem Description

Problem definition is taken from leetcode. 
- [Knight Probability in Chessboard](https://leetcode.com/problems/knight-probability-in-chessboard/ "Go to leetcode"){:target="_blank" rel="noopener"}


>On an NxN chessboard, a knight starts at the r-th row and c-th column and attempts to make exactly K moves. The rows and columns are 0 indexed, so the top-left square is (0, 0), and the bottom-right square is (N-1, N-1).

>A chess knight has 8 possible moves it can make, as illustrated below. Each move is two squares in a cardinal direction, then one square in an orthogonal direction.

>Each time the knight is to move, it chooses one of eight possible moves uniformly at random (even if the piece would go off the chessboard) and moves there.

>The knight continues moving until it has made exactly K moves or has moved off the chessboard. Return the probability that the knight remains on the board after it has stopped moving.

![knight on board](https://assets.leetcode.com/uploads/2018/10/12/knight.png)

#### Example 1:

```
Input: 3, 2, 0, 0
Output: 0.0625
Explanation: There are two moves (to (1,2), (2,1)) that will keep the knight on the board.
From each of those positions, there are also two moves that will keep the knight on the board.
The total probability the knight stays on the board is 0.0625.
```

## Solution
Possible solutions are:
- [Iterative Solution]({{ site.baseurl }}{% post_url 2020-10-22-leetcode-knight-probability-in-chessboard-iterative %})
- [Recursive Solution]({{ site.baseurl }}{% post_url 2020-10-22-leetcode-knight-probability-in-chessboard-recursive %})



