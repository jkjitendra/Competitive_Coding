# Unique Paths

## Problem Statement:

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return  *the number of possible unique paths that the robot can take to reach the bottom-right corner* .

The test cases are generated so that the answer will be less than or equal to `2 * 10<sup>9</sup>`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

<pre><strong>Input:</strong> m = 3, n = 7
<strong>Output:</strong> 28
</pre>

**Example 2:**

<pre><strong>Input:</strong> m = 3, n = 2
<strong>Output:</strong> 3
<strong>Explanation:</strong> From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down
</pre>

**Constraints:**

* `1 <= m, n <= 100`

## Solution:

#### Method 1:

```java
class Solution {
  public int uniquePaths(int m, int n) {
    if (m == 1 || n == 1) return 1;
    return uniquePaths(m - 1, n) + uniquePaths(m, n - 1);
  } 
}
```

#### Method 2:

```java
class Solution {
  public int uniquePaths(int m, int n) {
    long result = 1;
    int j = 1;
    for (int i = m; i <= (m+n-2); i++, j++) {
      result *= i;
      result /= j;
    }
    return (int)result;
  } 
}
```
