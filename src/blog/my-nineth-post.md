---
title: Data Structure & Algo - Leetcode 289 Game of Life.
date: 2020-05-16 00:15:00
excerpt:  This problem is about 2D array. Our goal is to create the next generation of cells in the 2D gird based on the rules implemented. Seemingly an easy problem but there are so many things to be learnt in order to solve it with efficiency. That's exactly why practice makes perfect, isn't it? 
type: post
blog: true
tags: 
- leetcode
---

According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

Any live cell with fewer than two live neighbors dies, as if caused by under-population.
Any live cell with two or three live neighbors lives on to the next generation.
Any live cell with more than three live neighbors dies, as if by over-population..
Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.
Write a function to compute the next state (after one update) of the board given its current state. The next state is created by applying the above rules simultaneously to every cell in the current state, where births and deaths occur simultaneously.
```
Example:

Input: 
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
Output: 
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```
**Follow up:**

1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.

2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?

#### O(MN) space solution

It is important to realise that simultaneous update of the 2D grid with the next generation will modify the original grid which we may lose track of the actual number of live neighbours. Therefore, one way to solve this is by duplicating the original 2D grid which will not be altered throughout the updating process. By checking the eight neighbours of an cell in the duplicated unmodified board, we can then change the original board to generate the next generation based on the given rules. 
While this problem can be solved by duplicating the original 2D grid, this requires O(MN) space. The O(MN) space complexity can be expensive as the board grows larger. Detailed implementation of this method can be found in its leetcode article with comprehensive explaination. (Cheers to the lovely tech community) :rocket:

#### Complexity Analysis

- Time Complexity: O(M×N), where M is the number of rows and N is the number of columns of the Board.

- Space Complexity:O(M×N), where M is the number of rows and N is the number of columns of the Board. This is the space occupied by the copy board we created initially.


#### O(1) space solution

This approach entails in place modification of the grid without the need for another copy of the original one. We can change the value of the call such that it is able to represent both the previous and new generation. To do so, we can make use of the binary representation number 0, 1, 2, 3. That is 0 as 0000, 1 as 0001, 2 as 0010 and 3 as 0011.

**Algorithm**
1. iteration of each cell in the 2D grid. Iteration of 2D grid can be done by:

```js
int row = board.size();
int col = board[0].size();
for(int i = 0; i < row; i++) {
    for(int j = 0; j < col; j++) {
        board[i][j] //each cell 
    }
}
```
2. Assign number 1, 2 or 3 to the original grid based on the rules for the game of life.
- Any live cell with fewer than two live neighbors dies, as if caused by under-population. Number 1 is used to mark the state of cell from live to dead.

- Any live cell with two or three live neighbors lives on to the next generation. Number 3 is used to mark the state of cell from live to remain as live.

- Any live cell with more than three live neighbors dies, as if by over-population. Number 1 is used as the state of cell change from live to dead.

- Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction. Number 2 is used to mark the state of cell from dead to live.

3. With the newly computed 2D grid, we are still able to accurately count the number of lives of the eight surrounding neighbours at each iteration by check: 

```js
if (board[x][y] &1) {
    lives++;
}
```

 The meaning of ( **`something &1`** ) returns a boolean result of 0 or 1 depending on the least significant bit of the **`something`**.
 E.g Binary representation of 1 as 0001 has 1 as its last bit which will return 1. Likewise, binary representation of 2 as 0010 has 0. As such, the state of previous state of cell is preserved even after modification.

 ![ ogl001's Photo ](/gol001.svg)

 To check the eight neighbours of a cell, we can make 2 vectors of integers covering the horizontal direction and the vertical direction respectively. 

 ```js
 vector<int> dx = {-1,-1,-1,0,1,1,1,0};
 vector<int> dy = {-1,0,1,1,1,0,-1,-1};

 for(int i=0; i<row;i++) {
    for(int j=0;j<col;j++){
        int lives = 0;
        for(int d = 0; d<8; d++) {
            int x = i + dx[d];
            int y = j + dy[d];
            if (x < 0 || y < 0 || x >= row || y >= col) continue;
            else if (board[x][y] & 1) {
                lives++;
            }
        }
    }
 }          
...
```
#### Demo of iteration for each row

![ ogl00's Photo ](/gol000.svg)

4. Iterate the new 2D grid and modify the number assigned according to its second lowest bit. For example, second lowest bit for the number 1 with binary representation as 0001 is 0, marking a dead cell in the next generation while cells updated to number 2 (binary: 0010) or 3 (binary: 0011) will live in the next generation. To examine each cell's second lowest bit, we use `board[i][j] >>= 1` which means the value of board[i][j] is being shifted by one bit to the right.

### Notes
There are quite a fair bit to digest in this problem using the in place solution. It is my first time making use of bit representation. It definitely didn't come intuitively. Glad that this gives me a little exposure to binary representation of numbers. The qusestion introduce operators like ` x & 1 ` and ` x >>= 1 `.It is one new topic I have yet started reading about it. The directional iteration is quite useful in such 2D grid problems so it's worth noting it down. 