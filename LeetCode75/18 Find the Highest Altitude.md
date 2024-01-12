# Find the Highest Altitude

## Problem Statement:

There is a biker going on a road trip. The road trip consists of `n + 1` points at different altitudes. The biker starts his trip on point `0` with altitude equal `0`.

You are given an integer array `gain` of length `n` where `gain[i]` is the **net gain in altitude** between points `i` and `i + 1` for all (`0 <= i < n)`. Return *the **highest altitude** of a point.*

**Example 1:**

<pre><strong>Input:</strong> gain = [-5,1,5,0,-7]
<strong>Output:</strong> 1
<strong>Explanation:</strong> The altitudes are [0,-5,-4,1,1,-6]. The highest is 1.
</pre>

**Example 2:**

<pre><strong>Input:</strong> gain = [-4,-3,-2,-1,4,3,2]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The altitudes are [0,-4,-7,-9,-10,-6,-3,-1]. The highest is 0.
</pre>

**Constraints:**

* `n == gain.length`
* `1 <= n <= 100`
* `-100 <= gain[i] <= 100`

## Solution:

#### Method 1:

```Java
    class Solution {
        public int largestAltitude(int[] gain) {
            int n = gain.length;
            int[] altitudeHeight = new int[n+1];
            int i = 0;
            altitudeHeight[0] = 0;
            for (; i < n; i++) {
                altitudeHeight[i+1] = gain[i] + altitudeHeight[i];
            }
            i = 0;
            int maxHeight = Integer.MIN_VALUE;
            for (; i <= n; i++) {
                if (maxHeight < altitudeHeight[i]) {
                    maxHeight = altitudeHeight[i];
                }
            }
            return maxHeight;
        }
    }
```



#### Method 2:

```Java
    class Solution {
        public int largestAltitude(int[] gain) {
            int sum = 0, maxAltitude = 0;
            for (int g: gain) {
                sum += g;
                maxAltitude = Math.max(maxAltitude, sum);
            }
            return maxAltitude;
        }
    }
```
