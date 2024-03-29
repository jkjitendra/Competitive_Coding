# Max Number of k-Sum Pairs

## Problem Statement:

You are given an integer array `nums` and an integer `k`.

In one operation, you can pick two numbers from the array whose sum equals `k` and remove them from the array.

Return  *the maximum number of operations you can perform on the array* .

**Example 1:**

<pre><strong>Input:</strong> nums = [1,2,3,4], k = 5
<strong>Output:</strong> 2
<strong>Explanation:</strong> Starting with nums = [1,2,3,4]:
- Remove numbers 1 and 4, then nums = [2,3]
- Remove numbers 2 and 3, then nums = []
There are no more pairs that sum up to 5, hence a total of 2 operations.</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [3,1,3,4,3], k = 6
<strong>Output:</strong> 1
<strong>Explanation:</strong> Starting with nums = [3,1,3,4,3]:
- Remove the first two 3's, then nums = [1,4,3]
There are no more pairs that sum up to 6, hence a total of 1 operation.</pre>

**Constraints:**

* `1 <= nums.length <= 10<sup>5</sup>`
* `1 <= nums[i] <= 10<sup>9</sup>`
* `1 <= k <= 10<sup>9</sup>`

## Solution:

#### Method 1:

```java
    class Solution {
        public int maxOperations(int[] nums, int k) {
            if (nums.length < 2) {
                return 0;
            }
            int filteredLength = 0;
            for(int num: nums) {
                if (num < k) {
                    nums[filteredLength++] = num;
                }
            }
            Arrays.sort(nums, 0, filteredLength);
            int leftIdx = 0, rightIdx = filteredLength-1, count = 0;
            while (leftIdx < rightIdx) {
                int sum = nums[leftIdx] + nums[rightIdx];
                if (sum == k) {
                    count++;
                    leftIdx++;
                    rightIdx--;
                } else if (sum < k) {
                    leftIdx++;
                } else if (sum > k) {
                    rightIdx--;
                }
            }
            return count;
        }
    }
```
