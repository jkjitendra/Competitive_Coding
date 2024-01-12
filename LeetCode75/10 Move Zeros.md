# Move Zeros

## Problem Statement:

Given an integer array `nums`, move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

**Note** that you must do this in-place without making a copy of the array.

**Example 1:**

<pre><strong>Input:</strong> nums = [0,1,0,3,12]
<strong>Output:</strong> [1,3,12,0,0]
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [0]
</pre>

**Constraints:**

* `1 <= nums.length <= 10<sup>4</sup>`
* -2 `<sup>`31 `</sup>` <= nums[i] <= 2 `<sup>`31 `</sup>` - 1

**Follow up:** Could you minimize the total number of operations done?

## Solution:

#### Method 1:

```java
    class Solution {
        public void moveZeroes(int[] nums) {
            int numsLength = nums.length;
            int currentIndex = 0;
            int i = 0;
            for (; i < numsLength; i++) {
                if (nums[i] != 0) {
                    nums[currentIndex] = nums[i];
                    currentIndex++;
                }
            }
            for(i = currentIndex; i < numsLength; i++) {
                nums[i] = 0;
            }
        }
    }
```
