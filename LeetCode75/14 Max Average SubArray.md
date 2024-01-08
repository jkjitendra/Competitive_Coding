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
        public double findMaxAverage(int[] nums, int k) {
            if (nums.length == 1 && k == 1) return nums[0];
            double avg = 0.0, max = -Double.MAX_VALUE;
            int i = 0, j, lastIndex = nums.length - k;

            while (i <= lastIndex) {
                j = i;
                double sum = 0.0;

                while (j < k+i) {
                    sum += nums[j];
                    j++;
                }

                avg = sum/k;
                i++;

                if (max < avg) {
                    max = avg;
                }
            }
            return max;
        }
    }


#### Method 2:

    class Solution {
        public double findMaxAverage(int[] nums, int k) {
            if (nums.length == 1 && k == 1) return nums[0];

            double sum = 0;
            int n = nums.length, currentIndex = k;
            for (int i = 0; i < k; i++) {
                sum += nums[i];
            }

            double maxVal = sum;
            while (currentIndex < n) {
                sum += nums[currentIndex] - nums[currentIndex-k];
                maxVal = Math.max(maxVal, sum);
                currentIndex++;
            }

            return maxVal/k;
        }
    }
