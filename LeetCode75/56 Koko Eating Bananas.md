# Koko Eating Bananas

## Problem Statement:

Koko loves to eat bananas. There are `n` piles of bananas, the `i<sup>th</sup>` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.

Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.

Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.

Return *the minimum integer* `k` *such that she can eat all the bananas within* `h`  *hours* .

**Example 1:**

<pre><strong>Input:</strong> piles = [3,6,7,11], h = 8
<strong>Output:</strong> 4
</pre>

**Example 2:**

<pre><strong>Input:</strong> piles = [30,11,23,4,20], h = 5
<strong>Output:</strong> 30
</pre>

**Example 3:**

<pre><strong>Input:</strong> piles = [30,11,23,4,20], h = 6
<strong>Output:</strong> 23
</pre>

**Constraints:**

* `1 <= piles.length <= 10<sup>4</sup>`
* `piles.length <= h <= 10<sup>9</sup>`
* `1 <= piles[i] <= 10<sup>9</sup>`

## Solution:

#### Method 1:

```java
class Solution {
  public int minEatingSpeed(int[] piles, int h) {
    int left = 1;
    int right = getMax(piles);

    while (left < right) {
      int mid = left + (right - left) / 2;
      if (canFinish(piles, h, mid)) {
        right = mid;
      } else {
        left = mid + 1;
      }
    }
    return left;
  }
  private boolean canFinish(int[] piles, int h, int speed) {
    int totalHours = 0;
    for (int pile : piles) {
     totalHours += (pile + speed - 1) / speed;
    }
    return totalHours <= h;
  }

  private int getMax(int[] piles) {
    int max = 0;
    for (int pile : piles) {
      max = Math.max(max, pile);
    }
    return max;
  }
}
```

#### Method 2:

```java
class Solution {
  public int minEatingSpeed(int[] piles, int h) {
    long totalBananas = 0;
    for (int pile : piles) {
      totalBananas += pile;
    }
    int left = (int) ((totalBananas - 1) / h) + 1;
    int right = (int) ((totalBananas - piles.length) / (h - piles.length + 1)) + 1;
  
    while (left < right) {
      int mid = left + (right - left) / 2;
      int totalHours = 0;
      for (int pile : piles) {
        totalHours += (pile - 1) / mid + 1;
      }
      if (totalHours > h) {
        left = mid + 1;
      }
      else right = mid;
    }
    return left;
  }
}
```
