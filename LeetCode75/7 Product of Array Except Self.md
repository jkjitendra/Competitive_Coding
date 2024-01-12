# Product of Array Except Self

## Problem Statement:

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,2,3,4]
<strong>Output:</strong> [24,12,8,6]
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [-1,1,0,-3,3]
<strong>Output:</strong> [0,0,9,0,0]
</pre>

**Constraints:**

* `2 <= nums.length <= 10<sup>5</sup>`
* `-30 <= nums[i] <= 30`
* The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

**Follow up:** Can you solve the problem in `O(1)` extra space complexity? (The output array **does not** count as extra space for space complexity analysis.)

## Solution

#### Method 1:

```java
    class Solution {
        public int[] productExceptSelf(int[] nums) {
            int n = nums.length;
            int[] totalProduct = new int[n];
            int total;
            for (inti = 0; i < n; i++) {
                total = 1;
                for (intj = 0; j < n; j++) {
                    if (i != j) {
                        total *= nums[j];
                    }
                }
                totalPoduct[i] = total;
            }
            return totalProduct;
        }
    }
```

#### Method 2:

```java
    classSolution {
        public int[] productExceptSelf(int[] nums) {
            int n = nums.length;
            int[] totalProduct = new int[n];
            totalProduct[0] = 1;
            int product = 1;
            for (inti = 1; i < n; i++) {
                product = nums[i-1] * product;
                totalProduct[i] = product;
            }
            product = 1;
            for (inti = n - 1; i >= 0; i--) {
                totalProduct[i] = product * totalProduct[i];
                product = nums[i] * product;
            }
            return totalProduct;
        }
    }
```
