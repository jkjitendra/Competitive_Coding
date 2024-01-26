# Nearest Exit From Entrance in Maze

## Problem Statement:

You are given an `m x n` matrix `maze` ( **0-indexed** ) with empty cells (represented as `'.'`) and walls (represented as `'+'`). You are also given the `entrance` of the maze, where `entrance = [entrance<sub>row</sub>, entrance<sub>col</sub>]` denotes the row and column of the cell you are initially standing at.

In one step, you can move one cell  **up** ,  **down** ,  **left** , or  **right** . You cannot step into a cell with a wall, and you cannot step outside the maze. Your goal is to find the **nearest exit** from the `entrance`. An **exit** is defined as an **empty cell** that is at the **border** of the `maze`. The `entrance` **does not count** as an exit.

Return *the **number of steps** in the shortest path from the *`entrance` * to the nearest exit, or * `-1` * if no such path exists* .

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/06/04/nearest1-grid.jpg)

<pre><strong>Input:</strong> maze = [["+","+",".","+"],[".",".",".","+"],["+","+","+","."]], entrance = [1,2]
<strong>Output:</strong> 1
<strong>Explanation:</strong> There are 3 exits in this maze at [1,0], [0,2], and [2,3].
Initially, you are at the entrance cell [1,2].
- You can reach [1,0] by moving 2 steps left.
- You can reach [0,2] by moving 1 step up.
It is impossible to reach [2,3] from the entrance.
Thus, the nearest exit is [0,2], which is 1 step away.
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/06/04/nearesr2-grid.jpg)

<pre><strong>Input:</strong> maze = [["+","+","+"],[".",".","."],["+","+","+"]], entrance = [1,0]
<strong>Output:</strong> 2
<strong>Explanation:</strong> There is 1 exit in this maze at [1,2].
[1,0] does not count as an exit since it is the entrance cell.
Initially, you are at the entrance cell [1,0].
- You can reach [1,2] by moving 2 steps right.
Thus, the nearest exit is [1,2], which is 2 steps away.
</pre>

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/06/04/nearest3-grid.jpg)

<pre><strong>Input:</strong> maze = [[".","+"]], entrance = [0,0]
<strong>Output:</strong> -1
<strong>Explanation:</strong> There are no exits in this maze.
</pre>

**Constraints:**

* `maze.length == m`
* `maze[i].length == n`
* `1 <= m, n <= 100`
* `maze[i][j]` is either `'.'` or `'+'`.
* `entrance.length == 2`
* `0 <= entrance<sub>row</sub> < m`
* `0 <= entrance<sub>col</sub> < n`
* `entrance` will always be an empty cell.

## Solution:

#### Method 1:

```java
class Solution {
  private static final int[][] DIRECTIONS = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
  public int nearestExit(char[][] maze, int[] entrance) {
    int row = maze.length;
    int column = maze[0].length;

    boolean[][] visited = new boolean[row][column];
    Queue<int[]> queue = new LinkedList<>();
    queue.offer(new int[]{entrance[0], entrance[1]});
    visited[entrance[0]][entrance[1]] = true;

    int steps = 0;
    while (!queue.isEmpty()) {
      int size = queue.size();
      for (int i = 0; i < size; i++) {
        int[] pos = queue.poll();
        for (int[] dir : DIRECTIONS) {
          int newRow = pos[0] + dir[0];
          int newCol = pos[1] + dir[1];
          if (newRow < 0 || newRow >= row || newCol < 0 ||
              newCol >= column || maze[newRow][newCol] == '+' ||
              visited[newRow][newCol]) 
            continue;
          if (newRow == 0 || newRow == row - 1 || newCol == 0 || newCol == column - 1) 
            return steps + 1;
          queue.offer(new int[]{newRow, newCol});
          visited[newRow][newCol] = true;
        }
      }
      steps++;
    }
    return -1;
  }
}
```

#### #MMethod 2:
