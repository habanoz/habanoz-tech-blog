---
title: "Leetcode: Simplify Path"
categories:
  - Python
  - leetcode
  - data structure
  - algorithms

tags:
  - Array
---

## Problem Description

Problem definition is taken from leetcode. 
- [Simplify Path](https://leetcode.com/problems/simplify-path/ "Go to leetcode"){:target="_blank" rel="noopener"}

> Given an absolute path for a file (Unix-style), simplify it. Or in other words, convert it to the canonical path.

> In a UNIX-style file system, a period '.' refers to the current directory. Furthermore, a double period '..' moves the directory up a level.

> Note that the returned canonical path must always begin with a slash '/', and there must be only a single slash '/' between two directory names. The last directory name (if it exists) must not end with a trailing '/'. Also, the canonical path must be the shortest string representing the absolute path.

### Example 1
```
Input: path = "/home/"
Output: "/home"
Explanation: Note that there is no trailing slash after the last directory name.
```

### Example 2
```
Input: path = "/../"
Output: "/"
Explanation: Going one level up from the root directory is a no-op, as the root level is the highest level you can go.
```

### Example 3
```
Input: path = "/home//foo/"
Output: "/home/foo"
Explanation: In the canonical path, multiple consecutive slashes are replaced by a single one.
```

### Example 4
```
Input: path = "/a/./b/../../c/"
Output: "/c"
```

### Example 5
```
Input: path = "/a/..hidden"
Output: "/a/..hidden"
```

### Example 6
```
Input: path = "/a/hidden.."
Output: "/a/hidden.."
```

## Solution 1

First solution uses an array large enough to keep all possible partitions.
slash_flag is used to avoid processing duplicate slashes.
pinter is used to point to position in buffer array. 

At each slash buffer pointer is incremented. There are two exceptions to this.
 - At Single dot, do not update pointer bu clean current buffer position.
 - At double dot, decrement buffer position and clear two positions.

Before exiting check current buffer for single or double dots.  

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        buffer = ['' for i in path]
        pointer= -1
        slash_flag=False
        
        for c in path:
            if c=='/':
                if not slash_flag:                   
                    slash_flag = True
                    if buffer[pointer]=='.':
                        buffer[pointer]=''
                    elif buffer[pointer]=='..':
                        pointer = self.work_on_dots(pointer, buffer)
                    else:
                        pointer=pointer+1
            else:
                slash_flag = False
                buffer[pointer]+=c
        
        if buffer[pointer]=='.':
            buffer[pointer]=''
        elif buffer[pointer]=='..':
            pointer = self.work_on_dots(pointer, buffer)
               
        return "/"+"/".join(c for c in buffer if c)
    
    def work_on_dots(self, pointer, buffer):
        pointer = max(0,pointer-1)
        buffer[pointer+1]=''
        buffer[pointer]=''
        return pointer
```

# Solution 2

Second solution follows a cleaner approach. Has the same cost with first approach.
List is used as a stack so that in case of '..' last element is easily removed.
Using split function and filtering single dot and empty values, makes buffer population easier.

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        tokens = [i for i in path.split('/') if i!='' and i!='.']
        buffer = []
        
        for token in tokens:
            if token=='..':
                if buffer: buffer.pop()
            else:
                buffer.append(token)     
        
        return "/"+"/".join(c for c in buffer if c)
```