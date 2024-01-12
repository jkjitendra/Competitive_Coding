# Find Pivot Index

## Problem Statement:

Given an array of integers `nums`, calculate the **pivot index** of this array.

The **pivot index** is the index where the sum of all the numbers **strictly** to the left of the index is equal to the sum of all the numbers **strictly** to the index's right.

If the index is on the left edge of the array, then the left sum is `0` because there are no elements to the left. This also applies to the right edge of the array.

Return  *the **leftmost pivot index*** . If no such index exists, return `-1`.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,7,3,6,5,6]
<strong>Output:</strong> 3
<strong>Explanation:</strong>
The pivot index is 3.
Left sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11
Right sum = nums[4] + nums[5] = 5 + 6 = 11
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> -1
<strong>Explanation:</strong>
There is no index that satisfies the conditions in the problem statement.</pre>

**Example 3:**

<pre><strong>Input:</strong> nums = [2,1,-1]
<strong>Output:</strong> 0
<strong>Explanation:</strong>
The pivot index is 0.
Left sum = 0 (no elements to the left of index 0)
Right sum = nums[1] + nums[2] = 1 + -1 = 0
</pre>

**Constraints:**

* `1 <= nums.length <= 10<sup>4</sup>`
* `-1000 <= nums[i] <= 1000`

## Solution:

#### Method 1:

```Java
    class Solution {
        public int pivotIndex(int[] nums) {
            int n = nums.length;
            int pivot = -1;
            if (n == 1) return 0;
            if (n == 2 && nums[1] == 0) return 0;
            int left = 0, right = 0;
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < i; j++) {
                    if (i != j) {
                        left += nums[j];
                    }
                }
                for (int k = i+1; k < n; k++) {
                    right += nums[k];
                }
                if (left == right) {
                    pivot = i;
                    break;
                }
                left = 0;
                right = 0;
            }
            return pivot;
        }
    }
```

#### Method 2:

```Java
    class Solution {
        public int pivotIndex(int[] nums) {
            int n = nums.length;
            int total = 0, leftSum = 0;
            for (int num: nums) {
                total += num;
            }  
            for (int i = 0; i < n; i++) {
                if (leftSum == (total - leftSum - nums[i])) return i;
                leftSum += nums[i];
            }
            return -1;
        }
    }
```
