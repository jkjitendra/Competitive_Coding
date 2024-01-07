# Max Average SubArray

## Problem Statement:

You are given an integer array `nums` consisting of `n` elements, and an integer `k`.

Find a contiguous subarray whose **length is equal to** `k` that has the maximum average value and return  *this value* . Any answer with a calculation error less than `10<sup>-5</sup>` will be accepted.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,12,-5,-6,50,3], k = 4
<strong>Output:</strong> 12.75000
<strong>Explanation:</strong> Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [5], k = 1
<strong>Output:</strong> 5.00000
</pre>

**Constraints:**

* `n == nums.length`
* `1 <= k <= n <= 10<sup>5</sup>`
* `-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>`


## Solution:

#### Method 1:

    class Solution {
        publicdoublefindMaxAverage(int[] nums, intk) {
            String[] strArray = s.split("\\s+");
            StringBuildersb = newStringBuilder();
            for ( inti = strArray.length - 1; i > 0; i--) {
                sb.append(strArray[i]).append(" ");
            }
            returnsb.append(strArray[0]).toString().trim();
        }
    }
