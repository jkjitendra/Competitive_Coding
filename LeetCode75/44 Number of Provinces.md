# Number of Provinces

## Problem Statement:

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `i<sup>th</sup>` city and the `j<sup>th</sup>` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return  *the total number of **provinces*** .

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

<pre><strong>Input:</strong> isConnected = [[1,1,0],[1,1,0],[0,0,1]]
<strong>Output:</strong> 2
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

<pre><strong>Input:</strong> isConnected = [[1,0,0],[0,1,0],[0,0,1]]
<strong>Output:</strong> 3
</pre>

**Constraints:**

* `1 <= n <= 200`
* `n == isConnected.length`
* `n == isConnected[i].length`
* `isConnected[i][j]` is `1` or `0`.
* `isConnected[i][i] == 1`
* `isConnected[i][j] == isConnected[j][i]`


## Solution:

#### Method 1:

```java
class Solution {
  public int findCircleNum(int[][] isConnected) {
    int totalProvinces = 0;
    int n = isConnected.length;
    for (int i = 0; i < n; i++) {
      if (isConnected[i][i] == 1) {
        totalProvinces++;
        checkIfConnected(isConnected, i, n);
      }
    }
    return totalProvinces;
  }

  public static void checkIfConnected(int[][] isConnected, int i, int n) {
    isConnected[i][i] = 0;
    for (int j = 0; j < n; j++) {
      if (isConnected[i][j] == 1) {
        isConnected[i][j] = 0;
        if (isConnected[j][j] == 1)
          checkIfConnected(isConnected, j, n);
      }
    }
  }
}
```
