# Successfull Pairs of Spells and Potions

## Problem Statement:

You are given two positive integer arrays `spells` and `potions`, of length `n` and `m` respectively, where `spells[i]` represents the strength of the `i<sup>th</sup>` spell and `potions[j]` represents the strength of the `j<sup>th</sup>` potion.

You are also given an integer `success`. A spell and potion pair is considered **successful** if the **product** of their strengths is **at least** `success`.

Return *an integer array *`pairs`* of length *`n`* where *`pairs[i]`* is the number of **potions** that will form a successful pair with the *`i<sup>th</sup>`* spell.*

**Example 1:**

<pre><strong>Input:</strong> spells = [5,1,3], potions = [1,2,3,4,5], success = 7
<strong>Output:</strong> [4,0,3]
<strong>Explanation:</strong>
- 0<sup>th</sup> spell: 5 * [1,2,3,4,5] = [5,<u><strong>10</strong></u>,<u><strong>15</strong></u>,<u><strong>20</strong></u>,<u><strong>25</strong></u>]. 4 pairs are successful.
- 1<sup>st</sup> spell: 1 * [1,2,3,4,5] = [1,2,3,4,5]. 0 pairs are successful.
- 2<sup>nd</sup> spell: 3 * [1,2,3,4,5] = [3,6,<u><strong>9</strong></u>,<u><strong>12</strong></u>,<u><strong>15</strong></u>]. 3 pairs are successful.
Thus, [4,0,3] is returned.
</pre>

**Example 2:**

<pre><strong>Input:</strong> spells = [3,1,2], potions = [8,5,8], success = 16
<strong>Output:</strong> [2,0,2]
<strong>Explanation:</strong>
- 0<sup>th</sup> spell: 3 * [8,5,8] = [<u><strong>24</strong></u>,15,<u><strong>24</strong></u>]. 2 pairs are successful.
- 1<sup>st</sup> spell: 1 * [8,5,8] = [8,5,8]. 0 pairs are successful. 
- 2<sup>nd</sup> spell: 2 * [8,5,8] = [<strong><u>16</u></strong>,10,<u><strong>16</strong></u>]. 2 pairs are successful. 
Thus, [2,0,2] is returned.
</pre>

**Constraints:**

* `n == spells.length`
* `m == potions.length`
* `1 <= n, m <= 10<sup>5</sup>`
* `1 <= spells[i], potions[i] <= 10<sup>5</sup>`
* `1 <= success <= 10<sup>10</sup>`


## Solution:

#### Method 1:

```java
class Solution {
  public int[] successfulPairs(int[] spells, int[] potions, long success) {
    int n = spells.length;
    int m = potions.length;
    int[] spellsPotionsPairs = new int[n];

    for (int i = 0; i < n; i++) {
      int count = 0;
      for (int j = 0; j < m; j++) {
        long prod = (long)spells[i] * potions[j];
        if (prod >= success) 
          count++;
      }
      spellsPotionsPairs[i] = count;
    }
    return spellsPotionsPairs;
  }
}
```


# Method 2:

```java
class Solution {
  public int[] successfulPairs(int[] spells, int[] potions, long success) {
    int n = spells.length;
    int m = potions.length;
    int[] spellsPotionsPairs = new int[n];
    Arrays.sort(potions);
    for (int i = 0; i < n; i++) {
      int left = 0, right = m - 1;
      int mid;
      while (left <= right) {
        mid = left + (right-left)/2;
        long prod = (long)spells[i] * potions[mid];
        if (prod >= success) 
          right = mid - 1;
        else
          left = mid + 1;
      }
      spellsPotionsPairs[i] = m - left;
    }
    return spellsPotionsPairs;
  }
}
```


#### Method 3:

```java
class Solution {
  public int[] successfulPairs(int[] spells, int[] potions, long success) {
    int maxPotion = 0;

    for (int potion : potions) 
      maxPotion = Math.max(maxPotion, potion);

    int[] sufficientPotion = new int[maxPotion + 1];

    for (int potion : potions) 
      sufficientPotion[potion]++;

    for (int i = sufficientPotion.length - 2; i >= 0; i--) 
      sufficientPotion[i] += sufficientPotion[i + 1];

    for (int i = 0; i < spells.length; i++) {
      int val = (int) Math.ceil((double) success / spells[i]);
      spells[i] = val > maxPotion ? 0 : sufficientPotion[(int)val];
    }
    return spells;
  }
}
```
