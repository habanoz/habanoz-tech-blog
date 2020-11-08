---
title: "Leetcode: Valid Sudoku"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
---

## Problem Description

Problem definition is taken from leetcode. 
- [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
> 1. Each row must contain the digits 1-9 without repetition.
> 2. Each column must contain the digits 1-9 without repetition.
> 3. Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.

### Example 1 
```
Input: board = 
[["5","3",".",".","7",".",".",".","."]
,["6",".",".","1","9","5",".",".","."]
,[".","9","8",".",".",".",".","6","."]
,["8",".",".",".","6",".",".",".","3"]
,["4",".",".","8",".","3",".",".","1"]
,["7",".",".",".","2",".",".",".","6"]
,[".","6",".",".",".",".","2","8","."]
,[".",".",".","4","1","9",".",".","5"]
,[".",".",".",".","8",".",".","7","9"]]
Output: true
```

## Solution

The algorithm iterates over the board 3x3 block-wise. i and j indices select the 3x3 block.ii and jj indices select the cell within the block. For each block, an array 's' , named after sub-block, is created. Array s is a single dimensional array which holds 1 at index 'd-1' for observed digit d.   

The algorithm keeps two 9x9 arrays to keep track of observed digits. If current cell is in row i*3+ii and cell value is digit 'd', 'horizontal' array at that row should have value zero at 'd-1'th index. Similarly, if current cell is in column j*3+jj and cell value is digit 'd', 'vertical' array at that column should have value zero at 'd-1'th index should have value 0.
You may be asking why index 'd-1'. Digit values range between 1-9 while array indices range between 0-8. For a correct mapping index is d-1.

Input size is always 9x9. A complexity analysis is not relevant. Each cell in the input array is visited only once. 

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        
        int[][] h = new int[9][9];
        int[][] v = new int[9][9];
        
        for(int i=0;i<3;i++){
            for(int j=0;j<3;j++){
                int[] s = new int[9];
                for(int ii=0;ii<3;ii++){
                    for(int jj=0;jj<3;jj++){
                        char c = board[i*3+ii][j*3+jj];
                        
                        if(c=='.'){
                            continue;
                        }
                        
                        int d = c-'0';
                        
                        if(s[d-1]!=0)return false;
                        s[d-1] = d;
                        
                        if(h[i*3+ii][d-1]!=0) return false;
                        h[i*3+ii][d-1] = 1;
                        
                        if(v[j*3+jj][d-1]!=0)return false;
                        v[j*3+jj][d-1] = 1;
                    }
                }                              
            }
        }
        
        return true;
    }
}
```
