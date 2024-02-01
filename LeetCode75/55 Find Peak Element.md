# Find Peak Element

## Problem Statement:

A peak element is an element that is strictly greater than its neighbors.

Given a **0-indexed** integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to  **any of the peaks** .

You may imagine that `nums[-1] = nums[n] = -∞`. In other words, an element is always considered to be strictly greater than a neighbor that is outside the array.

You must write an algorithm that runs in `O(log n)` time.

**Example 1:**

<pre><strong>Input:</strong> nums = [1,2,3,1]
<strong>Output:</strong> 2
<strong>Explanation:</strong> 3 is a peak element and your function should return the index number 2.</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [1,2,1,3,5,6,4]
<strong>Output:</strong> 5
<strong>Explanation:</strong> Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.</pre>

**Constraints:**

* `1 <= nums.length <= 1000`
* `-2<sup>31</sup> <= nums[i] <= 2<sup>31</sup> - 1`
* `nums[i] != nums[i + 1]` for all valid `i`.

## Solution:

#### Method 1:

```java
class Solution {
  public int findPeakElement(int[] nums) {
    int n = nums.length;
    for (int i = 0; i < n-1; i++) {
      if (nums[i] > nums[i+1]) {
        return i;
      }
    }
    return n - 1;
  }
}
```

#### Method 2:

```java
class Solution {
  public int findPeakElement(int[] nums) {
    int n = nums.length;
    if (n == 1 || nums[0] > nums[1]) return 0;
    if (nums[n-1] > nums[n-2]) return n-1;

    int left = 1, right = n-2;
    int mid;
    while (left <= right) {
      mid = left + (right-left)/2;
      if (nums[mid] > nums[mid-1] && nums[mid] > nums[mid+1]) return mid;
      else if (nums[mid] > nums[mid-1]) left = mid + 1;
      else right = mid - 1;
    }
    return -1;
  }
}
```
