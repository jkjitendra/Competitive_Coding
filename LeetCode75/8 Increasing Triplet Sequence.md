# Increasing Triplet Sequence

## Problem Statement:

Given an integer array `nums`, return `true` * if there exists a triple of indices * `(i, j, k)`* such that *`i < j < k`* and *`nums[i] < nums[j] < nums[k]`. If no such indices exists, return `false`.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,2,3,4,5]
<strong>Output:</strong> true
<strong>Explanation:</strong> Any triplet where i < j < k is valid.
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [5,4,3,2,1]
<strong>Output:</strong> false
<strong>Explanation:</strong> No triplet exists.
</pre>

**Example 3:**

<pre><strong>Input:</strong> nums = [2,1,5,0,4,6]
<strong>Output:</strong> true
<strong>Explanation:</strong> The triplet (3, 4, 5) is valid because nums[3] == 0 < nums[4] == 4 < nums[5] == 6.
</pre>

**Constraints:**

* `1 <= nums.length <= 5 * 10<sup>5</sup>`
* `-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1`

**Follow up:** Could you implement a solution that runs in `O(n)` time complexity and `O(1)` space complexity?

## Solution:

#### Method 1:

    class Solution {
        public boolean increasingTriplet(int[] nums) {
            int first = Integer.MAX_VALUE;
            int second = Integer.MAX_VALUE;
            for (int num: nums) {
                if (num <= first)
                    first = num;
                else if (num <= second)
                    second = num;
                else
                    return true;
            }
            return false;
        }
    }
