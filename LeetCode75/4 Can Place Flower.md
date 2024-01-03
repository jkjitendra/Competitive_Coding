# Can Place Flower


## Problem Statement:


You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in **adjacent** plots.

Given an integer array `flowerbed` containing `0`'s and `1`'s, where `0` means empty and `1` means not empty, and an integer `n`, return `true` *if* `n` *new flowers can be planted in the* `flowerbed` *without violating the no-adjacent-flowers rule and* `false`  *otherwise* .

**Example 1:**

<pre><strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 1
<strong>Output:</strong> true
</pre>

**Example 2:**

<pre><strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 2
<strong>Output:</strong> false
</pre>

**Constraints:**

* `1 <= flowerbed.length <= 2 * 10<sup>4</sup>`
* `flowerbed[i]` is `0` or `1`.
* There are no two adjacent flowers in `flowerbed`.
* `0 <= n <= flowerbed.length`



## Solution:

#### Method 1:

    class Solution {
        public boolean canPlaceFlowers(int[] flowerbed, int n) {
            int count = 0, i = 0;
            while (i < flowerbed.length) {
                 if ( flowerbed[i] == 0 &&                                   // is current position empty
                    (i == 0 || flowerbed[i - 1] == 0) &&                    // is previous position index 0 or previous position is empty
                    (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)   // is next position index last or next position is empty
                 ) {
                        flowerbed[i] = 1;
                        count++;
                    }
                 i++;
                 if (count >= n) return true;
            }
            return false;
        }
    }
