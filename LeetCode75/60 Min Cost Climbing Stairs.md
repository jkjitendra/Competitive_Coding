# Min Cost Climbing Stairs

## Problem Statement:

You are given an integer array `cost` where `cost[i]` is the cost of `i<sup>th</sup>` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return  *the minimum cost to reach the top of the floor* .

**Example 1:**

<pre><strong>Input:</strong> cost = [10,<u>15</u>,20]
<strong>Output:</strong> 15
<strong>Explanation:</strong> You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.
</pre>

**Example 2:**

<pre><strong>Input:</strong> cost = [<u>1</u>,100,<u>1</u>,1,<u>1</u>,100,<u>1</u>,<u>1</u>,100,<u>1</u>]
<strong>Output:</strong> 6
<strong>Explanation:</strong> You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.
</pre>

**Constraints:**

* `2 <= cost.length <= 1000`
* `0 <= cost[i] <= 999`

## Solution:

#### Method 1:

```java
class Solution {
  public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
        int[] dp = new int[n];
    
        dp[0] = cost[0];
        dp[1] = cost[1];
    
        for (int i = 2; i < n; i++) {
            dp[i] = Math.min(dp[i - 1], dp[i - 2]) + cost[i];
        }
    
        return Math.min(dp[n - 1], dp[n - 2]);
  }
}
```

#### Method 2:

```java

```
