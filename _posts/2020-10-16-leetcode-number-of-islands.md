---
title: "Leetcode: Number of Islands"
categories:
  - Java
  - leetcode
  - data structure
  - algorithms

tags:
  - depth-first-search
---

## Problem Description

Problem definition is taken from leetcode. 
- https://leetcode.com/problems/number-of-islands/

> Given an m x n 2d grid map of '1's (land) and '0's (water), return the number of islands.
> An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.


#### Example 1:

```
Input: grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
Output: 1
```

## Solution

Depth-first search is used to traverse the 2d search space. Use of a stack is preferred over recursion to avoid stack overflow. Once a '1' char is seen, search is expanded through lower, right, left and upper elements. Visited elements are marked with '0' char.

```java
class Solution {
    public int numIslands(char[][] grid) {
        char count=0;
        
        for(int i=0; i < grid.length;i++){
            for(int j=0; j < grid[0].length;j++){
                char val = grid[i][j];
                if(val=='1'){
                    Queue stack=new LinkedList();
                    
                    ++count;
                    grid[i][j] = '0';
                    traverse(grid, i, j, stack);
                    
                    while(!stack.isEmpty()){
                        int r = (int) stack.remove();
                        int c = (int) stack.remove();
                        traverse(grid,r, c, stack);
                    }
                }
            }
        }
        
        return count;
    }
    
    public void traverse(char[][] grid, int i, int j, Queue stack){
        // down
         if(i<grid.length-1 && grid[i+1][j] == '1'){
            grid[i+1][j] = '0';
            
            stack.add(i+1);
            stack.add(j);
         }
         
        //right
        if(j<grid[0].length-1 && grid[i][j+1] == '1'){
            grid[i][j+1] = '0';
            
            stack.add(i);
            stack.add(j+1);
        }
        
        if(j>0 && grid[i][j-1] == '1'){
            grid[i][j-1] = '0';
            
            stack.add(i);
            stack.add(j-1);
        }
        
        if(i>0 && grid[i-1][j] == '1'){
            grid[i-1][j] = '0';
            
            stack.add(i-1);
            stack.add(j);
        }
    }
    
} 
```

## Complexity Analysis

Search grid is m x n. All elements of the grid is visited sequentially. Growth is controlled by the search space dimensions. At each position 4 neighbours are visited.
Visited elements are marked and not traversed again. In summary, each element is visited once in the  main loop once and 4 more times when neighbours are traversed.
```
Time Complexity: O(mxn)+O(4xmxn) = O(mxn)
```



