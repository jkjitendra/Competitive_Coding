# House Robber

## Problem Statement:

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and  **it will automatically contact the police if two adjacent houses were broken into on the same night** .

Given an integer array `nums` representing the amount of money of each house, return  *the maximum amount of money you can rob tonight **without alerting the police*** .

**Example 1:**

<pre><strong>Input:</strong> nums = [1,2,3,1]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [2,7,9,3,1]
<strong>Output:</strong> 12
<strong>Explanation:</strong> Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
Total amount you can rob = 2 + 9 + 1 = 12.
</pre>

**Constraints:**

* `1 <= nums.length <= 100`
* `0 <= nums[i] <= 400`

## Solution:

#### Method 1:

```java
class Solution {
  int[] dp;
  public int rob(int[] nums) {
    int n = nums.length;
    dp = new int[n+1];
    for (int i = 0; i < n; i++) dp[i] = -1;
    return recursiveRob(nums, n-1);
  }

  private int recursiveRob(int[] nums, int n) {
    if (n < 0) return 0;
    if (dp[n] >= 0) return dp[n];
    int result = Math.max(recursiveRob(nums, n-2) + nums[n], recursiveRob(nums, n-1));
    dp[n] = result;
    return result;
  }
}
```

#### Method 2:

```java
class Solution {
  public int rob(int[] nums) {
    int n = nums.length;
    int prevAdjacent = 0, prevToPrevAdjacent = 0;

    for (int num: nums) {
      int temp = prevAdjacent;
      prevAdjacent = Math.max(prevToPrevAdjacent + num, prevAdjacent);
      prevToPrevAdjacent = temp;
    }
    return prevAdjacent;
  }
}
```
