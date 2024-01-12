# Maximum Consecutive Ones

## Problem Statement:

Given a binary array `nums` and an integer `k`, return *the maximum number of consecutive *`1`*'s in the array if you can flip at most* `k` `0`'s.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
<strong>Output:</strong> 6
<strong>Explanation:</strong> [1,1,1,0,0,<u><strong>1</strong>,1,1,1,1,<strong>1</strong></u>]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3
<strong>Output:</strong> 10
<strong>Explanation:</strong> [0,0,<u>1,1,<strong>1</strong>,<strong>1</strong>,1,1,1,<strong>1</strong>,1,1</u>,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.
</pre>

**Constraints:**

* `1 <= nums.length <= 10<sup>5</sup>`
* `nums[i]` is either `0` or `1`.
* `0 <= k <= nums.length`

## Solution:

#### Method 1:

```java
    class Solution {
        public int longestOnes(int[] nums, int k) {
            int n = nums.length;
            int startOfWindow = 0, endOfWindow = 0;
            int maxNoOfConsecutiveOnes = 0;
            int flippedCount = k;
            while (endOfWindow < n) {
                if (nums[endOfWindow] == 0) {
                    flippedCount--;
                }
                while (flippedCount < 0) {
                    if (nums[startOfWindow] == 0) {
                        flippedCount++;
                    }
                    startOfWindow++;
                }
                maxNoOfConsecutiveOnes = Math.max(maxNoOfConsecutiveOnes, endOfWindow - startOfWindow + 1);
                endOfWindow++;
            }
            return maxNoOfConsecutiveOnes;
        }
    }
```

#### Method 2:

```java
    class Solution {
        public int longestOnes(int[] nums, int k) {
            int n = nums.length;
            int startOfWindow = 0, endOfWindow = 0;
            int flippedCount = k;
            while (endOfWindow < n) {
                if (nums[endOfWindow] == 0) {
                    flippedCount--;
                }
                if (flippedCount < 0 && nums[startOfWindow++] == 0) {
                    flippedCount++;
                }
                endOfWindow++;
            }
            return endOfWindow - startOfWindow;
        }
    }
```
