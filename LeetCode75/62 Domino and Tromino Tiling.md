# Domino and Tromino Tiling

## Problem Statement:

You have two types of tiles: a `2 x 1` domino shape and a tromino shape. You may rotate these shapes.

![](https://assets.leetcode.com/uploads/2021/07/15/lc-domino.jpg)

Given an integer n, return *the number of ways to tile an* `2 x n`  *board* . Since the answer may be very large, return it **modulo** `10<sup>9</sup> + 7`.

In a tiling, every square must be covered by a tile. Two tilings are different if and only if there are two 4-directionally adjacent cells on the board such that exactly one of the tilings has both squares occupied by a tile.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/15/lc-domino1.jpg)

<pre><strong>Input:</strong> n = 3
<strong>Output:</strong> 5
<strong>Explanation:</strong> The five different ways are show above.
</pre>

**Example 2:**

<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> 1
</pre>

**Constraints:**

* `1 <= n <= 1000`

## Solution:

#### Method 1:

```java
class Solution {
  private static final int MOD = 1000000007;

  public int numTilings(int n) {
    if (n <= 2) return n;
    long[] dp = new long[n+1];
    dp[0] = 1;
    dp[1] = 1;
    dp[2] = 2;
    if (n <= 2) return (int)dp[n];
    int i = 3;
    while (i <= n) {
      dp[i] = (dp[i-1]*2 + dp[i-3]) % MOD;
      i++;
    }
    return (int)dp[n];
  }
}
```
