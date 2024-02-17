# Non-Overlapping Intervals

## Problem Statement:

Given an array of intervals `intervals` where `intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]`, return  *the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping* .

**Example 1:**

<pre><strong>Input:</strong> intervals = [[1,2],[2,3],[3,4],[1,3]]
<strong>Output:</strong> 1
<strong>Explanation:</strong> [1,3] can be removed and the rest of the intervals are non-overlapping.
</pre>

**Example 2:**

<pre><strong>Input:</strong> intervals = [[1,2],[1,2],[1,2]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> You need to remove two [1,2] to make the rest of the intervals non-overlapping.
</pre>

**Example 3:**

<pre><strong>Input:</strong> intervals = [[1,2],[2,3]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> You don't need to remove any of the intervals since they're already non-overlapping.
</pre>

**Constraints:**

* `1 <= intervals.length <= 10<sup>5</sup>`
* `intervals[i].length == 2`
* `-5 * 10<sup>4</sup> <= start<sub>i</sub> < end<sub>i</sub> <= 5 * 10<sup>4</sup>`

## Solution:

#### Method 1:

```java
Arrays.sort(intervals, (a, b) -> Integer.compare(a[1], b[1]));
    int end = Integer.MIN_VALUE;
    int removeCount = 0;
  
    for (int[] interval : intervals) {
      if (interval[0] < end) {
        removeCount++;
      } else {
        end = interval[1];
      }
    }
    return removeCount;
  }
```

#### Method 2:

```java
class Solution {
  public int eraseOverlapIntervals(int[][] intervals) {

    int maxEndTime = intervals[0][1];
    int minEndTime = maxEndTime;

    // maximum and minimum end times
    for(int i = 1;i<intervals.length;i++){
      maxEndTime = Math.max(maxEndTime, intervals[i][1]);
      minEndTime = Math.min(minEndTime, intervals[i][1]);
    }
    // Calculate shift to make all numbers positive and create a range starting from 1
    int shift = 1 - minEndTime;
    // Determine the size of the array needed to track the farthest start times for each end time
    int intervalRange = 2 + maxEndTime - minEndTime; // +2 for inclusive ends and to start from 1

    // Array to track the farthest start time for each end time
    int[] farthestStartsForEnds = new int[intervalRange];

    // Populate the array with the farthest start times
    for (int[] interval : intervals) {
      int shiftedStart = interval[0] + shift;
      int shiftedEnd = interval[1] + shift;
      if (shiftedStart > farthestStartsForEnds[shiftedEnd]) 
        farthestStartsForEnds[shiftedEnd] = shiftedStart;
    }
    // Count the maximum number of non-overlapping intervals
    int lastEndIndex = 1; // Tracks the end of the last added interval to the non-overlapping set
    int nonOverlapCount = 1; // At least one interval doesn't overlap by default

    // Iterate through the array to find non-overlapping intervals
    for (int endIndex = 2; endIndex < intervalRange; endIndex++) {
      if (lastEndIndex <= farthestStartsForEnds[endIndex]) {
        nonOverlapCount++;
        lastEndIndex = endIndex; // Update the end of the last non-overlapping interval
      }
    }
    // The number of intervals to remove is the difference of intervalsLength and the count of non-overlapping intervals
    return intervals.length - nonOverlapCount;
  }
}
```
