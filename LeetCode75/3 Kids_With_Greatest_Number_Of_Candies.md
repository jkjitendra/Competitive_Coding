# Kids With Greatest Number of Candies

## Problem Statement:

There are `n` kids with candies. You are given an integer array `candies`, where each `candies[i]` represents the number of candies the `i<sup>th</sup>` kid has,

and an integer `extraCandies`, denoting the number of extra candies that you have.

Return a boolean array *`result`* of length *`n`*, where *`result[i]`* is *`true`* if, after giving the *`i<sup>th</sup>`* kid all the `extraCandies` *,*

*they will have the **greatest** number of candies among all the kids*, or *`false` otherwise* .

Note that **multiple** kids can have the **greatest** number of candies.

**Example 1:**

<pre><strong>Input:</strong> candies = [2,3,5,1,3], extraCandies = 3
<strong>Output:</strong> [true,true,true,false,true]

<strong>Explanation:</strong> If you give all extraCandies to:
- Kid 1, they will have 2 + 3 = 5 candies, which is the greatest among the kids.
- Kid 2, they will have 3 + 3 = 6 candies, which is the greatest among the kids.
- Kid 3, they will have 5 + 3 = 8 candies, which is the greatest among the kids.
- Kid 4, they will have 1 + 3 = 4 candies, which is not the greatest among the kids.
- Kid 5, they will have 3 + 3 = 6 candies, which is the greatest among the kids.
</pre>

**Example 2:**

<pre><strong>Input:</strong> candies = [4,2,1,1,2], extraCandies = 1
<strong>Output:</strong> [true,false,false,false,false]

<strong>Explanation:</strong> There is only 1 extra candy.
Kid 1 will always have the greatest number of candies, even if a different kid is given the extra candy.
</pre>

**Example 3:**

<pre><strong>Input:</strong> candies = [12,1,12], extraCandies = 10
<strong>Output:</strong> [true,false,true]
</pre>

**Constraints:**

* `n == candies.length`
* `2 <= n <= 100`
* `1 <= candies[i] <= 100`
* `1 <= extraCandies <= 50`

## Java Solution:-

#### Method 1:-

    class Solution {
        public List`<Boolean>` kidsWithCandies(int[] candies, int extraCandies) {
            int candiesLength = candies.length;
            boolean flag = true;
            List `<Boolean>` boolCandies = new ArrayList();
            for (int i = 0; i < candiesLength; i++) {
                int num = candies[i];
                int addedCandies = num + extraCandies;
                for (int j = 0; j < candiesLength; j++) {
                    if (i == j) continue;
                    if (addedCandies < candies[j]) {
                        flag = false;
                        break;
                    }
                }
                boolCandies.add(flag);
                flag=true;
            }
            return boolCandies;
        }
    }

#### Method 2:


    class Solution {
        public List`<Boolean>` kidsWithCandies(int[] candies, int extraCandies) {
            int candiesLength = candies.length;
            int max = 0;
            List `<Boolean>` boolCandies = new ArrayList();
            for (int candy: candies) {
                max = max > candy ? max : candy;
            }
            for (int i = 0; i < candiesLength; i++) {
                if ((candies[i] + extraCandies) < max) {
                    boolCandies.add(false);
                    continue;
                }
                boolCandies.add(true);
            }
            return boolCandies;
        }
    }
