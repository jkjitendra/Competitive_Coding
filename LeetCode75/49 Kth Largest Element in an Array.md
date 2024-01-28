# Kth Largest Element in an Array

## Problem Statement:

Given an integer array `nums` and an integer `k`, return *the* `k<sup>th</sup>`  *largest element in the array* .

Note that it is the `k<sup>th</sup>` largest element in the sorted order, not the `k<sup>th</sup>` distinct element.

Can you solve it without sorting?

**Example 1:**

<pre><strong>Input:</strong> nums = [3,2,1,5,6,4], k = 2
<strong>Output:</strong> 5
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums = [3,2,3,1,2,4,5,5,6], k = 4
<strong>Output:</strong> 4
</pre>

**Constraints:**

* `1 <= k <= nums.length <= 10<sup>5</sup>`
* `-10<sup>4</sup> <= nums[i] <= 10<sup>4</sup>`


## Solution:

#### Method 1:

```java
public class Solution {
  public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>(k);
    for (int num : nums) {
      pq.add(num);
      if (pq.size() > k) {
        pq.poll();
      }
    }
    return pq.peek();
  }
}

```

#### Method 2:

```java
public class Solution {
  public int findKthLargest(int[] nums, int k) {
    int[] countArray = new int[2 * 10000 + 1];
    int offset = 10000;

    for (int num : nums) {
      countArray[num + offset]++;
    }

    int n = countArray.length - 1;
    while (k > 0) {
      k -= countArray[n];
      n--;
    }

    return n - offset + 1;
  }
}

```
