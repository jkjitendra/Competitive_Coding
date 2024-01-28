# Rotting oranges

## Problem Statement:

You are given an `m x n` `grid` where each cell can have one of three values:

* `0` representing an empty cell,
* `1` representing a fresh orange, or
* `2` representing a rotten orange.

Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.

Return  *the minimum number of minutes that must elapse until no cell has a fresh orange* . If *this is impossible, return* `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

<pre><strong>Input:</strong> grid = [[2,1,1],[1,1,0],[0,1,1]]
<strong>Output:</strong> 4
</pre>

**Example 2:**

<pre><strong>Input:</strong> grid = [[2,1,1],[0,1,1],[1,0,1]]
<strong>Output:</strong> -1
<strong>Explanation:</strong> The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
</pre>

**Example 3:**

<pre><strong>Input:</strong> grid = [[0,2]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> Since there are already no fresh oranges at minute 0, the answer is just 0.
</pre>

**Constraints:**

* `m == grid.length`
* `n == grid[i].length`
* `1 <= m, n <= 10`
* `grid[i][j]` is `0`, `1`, or `2`.


## Solution:

#### Method 1:

```java
class Solution {
  public int orangesRotting(int[][] grid) {
    int row = grid.length;
    int column = grid[0].length;
    ArrayDeque<int[]> rottenOrangesQueue = new ArrayDeque<>();
    int freshOrangesCount = 0;
    int[][] directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
  
    for (int i = 0; i < row; i++) {
      for (int j = 0; j < column; j++) {
        if (grid[i][j] == 2) {
          rottenOrangesQueue.offer(new int[]{i, j});
        } else if (grid[i][j] == 1) {
          freshOrangesCount++;
        }
      }
    }
  
    if (freshOrangesCount == 0) return 0;
    int count = 0;
    while (!rottenOrangesQueue.isEmpty()) {
      int size = rottenOrangesQueue.size();
      for (int i = 0; i < size; i++) {
        int[] position = rottenOrangesQueue.poll();
        for (int[] direction : directions) {
          int x = position[0] + direction[0];
          int y = position[1] + direction[1];
          if (x < 0 || y < 0 || x >= row || y >= column || grid[x][y] != 1) 
            continue;
          grid[x][y] = 2;
          rottenOrangesQueue.offer(new int[]{x, y});
          freshOrangesCount--;
        }
      }
      count++;
    }
    return freshOrangesCount == 0 ? count - 1 : -1;
  }
}

```
