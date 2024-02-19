# Minimum Number of Arrows to Burst Balloons

## Problem Statement:

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [x<sub>start</sub>, x<sub>end</sub>]` denotes a balloon whose **horizontal diameter** stretches between `x<sub>start</sub>` and `x<sub>end</sub>`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up **directly vertically** (in the positive y-direction) from different points along the x-axis. A balloon with `x<sub>start</sub>` and `x<sub>end</sub>` is **burst** by an arrow shot at `x` if `x<sub>start</sub> <= x <= x<sub>end</sub>`. There is **no limit** to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return  *the **minimum** number of arrows that must be shot to burst all balloons* .

**Example 1:**

<pre><strong>Input:</strong> points = [[10,16],[2,8],[1,6],[7,12]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].
</pre>

**Example 2:**

<pre><strong>Input:</strong> points = [[1,2],[3,4],[5,6],[7,8]]
<strong>Output:</strong> 4
<strong>Explanation:</strong> One arrow needs to be shot for each balloon for a total of 4 arrows.
</pre>

**Example 3:**

<pre><strong>Input:</strong> points = [[1,2],[2,3],[3,4],[4,5]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 2, bursting the balloons [1,2] and [2,3].
- Shoot an arrow at x = 4, bursting the balloons [3,4] and [4,5].
</pre>

**Constraints:**

* `1 <= points.length <= 10<sup>5</sup>`
* `points[i].length == 2`
* `-2<sup>31</sup> <= x<sub>start</sub> < x<sub>end</sub> <= 2<sup>31</sup> - 1`

## Solution:

#### Method 1:

```java
class Solution {
  public int findMinArrowShots(int[][] points) {
    if (points.length == 0) return 0;
  
    // Sort the points by their end value
    Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));
  
    // Initialize arrows needed and the end point of the last burst balloon
    int arrows = 1;
    int lastEnd = points[0][1];
  
    // Iterate through the balloons
    for (int i = 1; i < points.length; i++) {
      // If the current balloon starts after the lastEnd, it needs a new arrow
      if (points[i][0] > lastEnd) {
        arrows++;
        lastEnd = points[i][1]; // Update lastEnd to the end of the current balloon
      }
    }
  
    // Return the total arrows needed
    return arrows;
  }
}
```
