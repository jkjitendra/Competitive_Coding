# Equal Row and Column Pairs

## Problem Statement:

Given a **0-indexed** `n x n` integer matrix `grid`,  *return the number of pairs * `(r<sub>i</sub>, c<sub>j</sub>)`* such that row *`r<sub>i</sub>`* and column *`c<sub>j</sub>` * are equal* .

A row and column pair is considered equal if they contain the same elements in the same order (i.e., an equal array).

**Example 1:**

![](https://assets.leetcode.com/uploads/2022/06/01/ex1.jpg)

<pre><strong>Input:</strong> grid = [[3,2,1],[1,7,6],[2,7,7]]
<strong>Output:</strong> 1
<strong>Explanation:</strong> There is 1 equal row and column pair:
- (Row 2, Column 1): [2,7,7]
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2022/06/01/ex2.jpg)

<pre><strong>Input:</strong> grid = [[3,1,2,2],[1,4,4,5],[2,4,2,2],[2,4,2,2]]
<strong>Output:</strong> 3
<strong>Explanation:</strong> There are 3 equal row and column pairs:
- (Row 0, Column 0): [3,1,2,2]
- (Row 2, Column 2): [2,4,2,2]
- (Row 3, Column 2): [2,4,2,2]
</pre>

**Constraints:**

* `n == grid.length == grid[i].length`
* `1 <= n <= 200`
* `1 <= grid[i][j] <= 10<sup>5</sup>`


## Solution:

#### Method 1:

```java
import java.util.Map.Entry;

class Solution {
  public int equalPairs(int[][] grid) {
    int n = grid.length;
    Map<String, Integer> rowMap = new HashMap<>();
    int count = 0;
    for (int i = 0; i < n; i++) {
      String temp = "";
      for (int j = 0; j < n; j++) {
        temp += grid[i][j] + ".";
      }
      rowMap.put(temp, rowMap.getOrDefault(temp, 0) + 1);
    }
    for (int i = 0; i < n; i++) {
      String temp = "";
      for (int j = 0; j < n; j++) {
        temp += grid[j][i] + ".";
      }
      if (rowMap.containsKey(temp)) {
        count += rowMap.get(temp);
      }
    }

    return count;
  }
}
```



#### Method 2:

```java
class Solution {
  public int equalPairs(int[][] grid) {
    HashMap<Integer, Integer> columnMap = new HashMap<>();
    int n = grid.length;
    int totalEqualPairs = 0;

    for (int row = 0; row < n; row++) {
      int hash = calculateColumnHash(row, grid, n);
      columnMap.put(hash, columnMap.getOrDefault(hash, 0) + 1);
    }

    for (int i = 0; i < n; i++) {
      int has = calculateRowHash(i, grid, n);
      totalEqualPairs += columnMap.getOrDefault(has, 0);
    }
    return totalEqualPairs;
  }

  private int calculateColumnHash(int row, int[][] grid, int n) {
    int hash = 0;
    for (int column = 0; column < n; column++) {
      hash = grid[column][row] + (17 * hash);
    }
    return hash;
  }

  private int calculateRowHash(int row, int[][] grid, int n) {
    int hash = 0;
    for (int column = 0; column < n; column++) {
      hash = grid[row][column] + (17 * hash);
    }
    return hash;
  }
}
```
