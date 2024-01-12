# Longest Subarray of 1's After Deleting One Element

## Problem Statement:

Given a binary array `nums`, you should delete one element from it.

Return *the size of the longest non-empty subarray containing only *`1` *'s in the resulting array* . Return `0` if there is no such subarray.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,1,0,1]
<strong>Output:</strong> 3
<strong>Explanation:</strong> After deleting the number in position 2, [1,1,1] contains 3 numbers with value of 1's.
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [0,1,1,1,0,1,1,0,1]
<strong>Output:</strong> 5
<strong>Explanation:</strong> After deleting the number in position 4, [0,1,1,1,1,1,0,1] longest subarray with value of 1's is [1,1,1,1,1].
</pre>

**Example 3:**

<pre><strong>Input:</strong> nums = [1,1,1]
<strong>Output:</strong> 2
<strong>Explanation:</strong> You must delete one element.
</pre>

**Constraints:**

* `1 <= nums.length <= 10<sup>5</sup>`
* `nums[i]` is either `0` or `1`.

## Solution:

#### Method 1:

```Java
   class Solution {
        public int longestOnes(int[] nums, int k) {
            int n = nums.length;
            int startOfWindow = 0, endOfWindow = 0;
            int zerosEncountered = k;
            while (endOfWindow < n) {
                if (nums[endOfWindow] == 0) {
                   zerosEncountered--;
                }
                if (zerosEncountered < 0 && nums[startOfWindow++] == 0) {
                    zerosEncountered++;
                }
                endOfWindow++;
            }
            return endOfWindow - startOfWindow;
        }
    }
```
