# Maximum Subsequence Score

## Problem Statement:

You are given two **0-indexed** integer arrays `nums1` and `nums2` of equal length `n` and a positive integer `k`. You must choose a **subsequence** of indices from `nums1` of length `k`.

For chosen indices `i<sub>0</sub>`, `i<sub>1</sub>`, ..., `i<sub>k - 1</sub>`, your **score** is defined as:

* The sum of the selected elements from `nums1` multiplied with the **minimum** of the selected elements from `nums2`.
* It can defined simply as: `(nums1[i<sub>0</sub>] + nums1[i<sub>1</sub>] +...+ nums1[i<sub>k - 1</sub>]) * min(nums2[i<sub>0</sub>] , nums2[i<sub>1</sub>], ... ,nums2[i<sub>k - 1</sub>])`.

Return *the **maximum** possible score.*

A **subsequence** of indices of an array is a set that can be derived from the set `{0, 1, ..., n-1}` by deleting some or no elements.

**Example 1:**

<pre><strong>Input:</strong> nums1 = [1,3,3,2], nums2 = [2,1,3,4], k = 3
<strong>Output:</strong> 12
<strong>Explanation:</strong> 
The four possible subsequence scores are:
- We choose the indices 0, 1, and 2 with score = (1+3+3) * min(2,1,3) = 7.
- We choose the indices 0, 1, and 3 with score = (1+3+2) * min(2,1,4) = 6. 
- We choose the indices 0, 2, and 3 with score = (1+3+2) * min(2,3,4) = 12. 
- We choose the indices 1, 2, and 3 with score = (3+3+2) * min(1,3,4) = 8.
Therefore, we return the max score, which is 12.
</pre>

**Example 2:**

<pre><strong>Input:</strong> nums1 = [4,2,3,1,1], nums2 = [7,5,10,9,6], k = 1
<strong>Output:</strong> 30
<strong>Explanation:</strong> 
Choosing index 2 is optimal: nums1[2] * nums2[2] = 3 * 10 = 30 is the maximum possible score.
</pre>

**Constraints:**

* `n == nums1.length == nums2.length`
* `1 <= n <= 10<sup>5</sup>`
* `0 <= nums1[i], nums2[j] <= 10<sup>5</sup>`
* `1 <= k <= n`

## Solution:

#### Method 1:

```java
class Solution {
  public long maxScore(int[] nums1, int[] nums2, int k) {
    int[][] valuePairs = pairValues(nums1, nums2);
    Arrays.sort(valuePairs, (a, b) -> b[0] - a[0]);

    PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    long currentSum = 0;
    long maxScore = 0;

    for (int[] pair : valuePairs) {
      int valueFromNums1 = pair[1];
      minHeap.add(valueFromNums1);
      currentSum += valueFromNums1;

      if (minHeap.size() > k) {
        currentSum -= minHeap.poll();
      }

      if (minHeap.size() == k) {
        maxScore = Math.max(maxScore, currentSum * pair[0]);
      }
    }
    return maxScore;
  }

  private int[][] pairValues(int[] nums1, int[] nums2) {
    int n = nums1.length;
    int[][] pairs = new int[n][2];
    for (int i = 0; i < n; i++) {
      pairs[i] = new int[] { nums2[i], nums1[i] };
    }
    return pairs;
  }
}

```

#### Method 2:

```java
class Solution {
  public long maxScore(int[] nums1, int[] nums2, int k) {
    int maxNum2Value = findMax(nums2);
  
    List<Integer>[] nums1ValuesGroupedByNums2 = new List[maxNum2Value + 1];
    for (int i = 0; i < nums1.length; ++i) {
      if (nums1ValuesGroupedByNums2[nums2[i]] == null) {
        nums1ValuesGroupedByNums2[nums2[i]] = new ArrayList<>();
      }
      nums1ValuesGroupedByNums2[nums2[i]].add(nums1[i]);
    }
  
    int maxNum1Value = findMax(nums1);
    int[] nums1ValueCount = new int[maxNum1Value + 1];
    int minNum1ValueSeen = -1;
  
    long currentSum = 0, maxScore = 0;
    for (int currentNum2Value = maxNum2Value; currentNum2Value >= 0; --currentNum2Value) {
      if (nums1ValuesGroupedByNums2[currentNum2Value] == null) 
        continue;
      for (int currentNum1Value : nums1ValuesGroupedByNums2[currentNum2Value]) {
        if (currentNum1Value < minNum1ValueSeen)
          continue;
    
        nums1ValueCount[currentNum1Value]++;
        currentSum += currentNum1Value;
    
        if (--k <= 0) {
          maxScore = Math.max(maxScore, currentSum * currentNum2Value);
          minNum1ValueSeen = updateMinNum1ValueSeen(nums1ValueCount, minNum1ValueSeen);
          currentSum -= minNum1ValueSeen;
        }
      }
    }
    return maxScore;
  }

  private int findMax(int[] nums) {
    int max = 0;
    for (int num : nums) {
      max = Math.max(max, num);
    }
    return max;
  }

  private int updateMinNum1ValueSeen(int[] nums1ValueCount, int minNum1ValueSeen) {
    if (minNum1ValueSeen == -1) {
      minNum1ValueSeen++;
    }
    while (nums1ValueCount[minNum1ValueSeen] == 0) {
      minNum1ValueSeen++;
    }
    nums1ValueCount[minNum1ValueSeen]--;
    return minNum1ValueSeen;
  }
}

```
