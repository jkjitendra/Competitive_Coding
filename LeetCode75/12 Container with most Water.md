# Container with most Water

## Problem Statement:

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `i<sup>th</sup>` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return  *the maximum amount of water a container can store* .

**Notice** that you may not slant the container.

**Example 1:**

![](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

<pre><strong>Input:</strong> height = [1,8,6,2,5,4,8,3,7]
<strong>Output:</strong> 49
<strong>Explanation:</strong> The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.
</pre>

**Example 2:**

<pre><strong>Input:</strong> height = [1,1]
<strong>Output:</strong> 1
</pre>

**Constraints:**

* `n == height.length`
* `2 <= n <= 10<sup>5</sup>`
* `0 <= height[i] <= 10<sup>4</sup>`

## Solution:

#### Method 1:

    class Solution {
        public int maxArea(int[] height) {
            int leftIdx = 0, rightIdx = height.length - 1;
            int max = 0, minHeight;

            while (leftIdx < rightIdx){
                minHeight = Math.min(height[leftIdx], height[rightIdx]);
                max = Math.max(max, minHeight * (rightIdx - leftIdx));

                while(leftIdx < rightIdx && height[leftIdx] <= minHeight) {
                    leftIdx++;
                }

                while(leftIdx < rightIdx && height[leftIdx] <= minHeight) {
                    rightIdx--;
                }
            }
            return max;
        }
    }
