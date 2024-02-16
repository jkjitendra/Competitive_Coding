# Minimum Flip to Make a OR b Equal to c

## Problem Statement:

Given 3 positives numbers `a`, `b` and `c`. Return the minimum flips required in some bits of `a` and `b` to make ( `a` OR `b` == `c` ). (bitwise OR operation).
Flip operation consists of change **any** single bit 1 to 0 or change the bit 0 to 1 in their binary representation.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/01/06/sample_3_1676.png)

<pre><strong>Input:</strong> a = 2, b = 6, c = 5
<strong>Output:</strong> 3
<strong>Explanation: </strong>After flips a = 1 , b = 4 , c = 5 such that (<code>a</code> OR <code>b</code> == <code>c</code>)</pre>

**Example 2:**

<pre><strong>Input:</strong> a = 4, b = 2, c = 7
<strong>Output:</strong> 1
</pre>

**Example 3:**

<pre><strong>Input:</strong> a = 1, b = 2, c = 3
<strong>Output:</strong> 0
</pre>

**Constraints:**

* `1 <= a <= 10^9`
* `1 <= b <= 10^9`
* `1 <= c <= 10^9`

## Solution:

#### Method 1:

```java
class Solution {
  public int minFlips(int a, int b, int c) {
    int aAndNotC = (a & ~c) ;
    int notABAndC = (~(a | b) & c) ;
    int bAndNotC = (b & ~c) ;
    return Integer.bitCount(aAndNotC) + Integer.bitCount(notABAndC) + Integer.bitCount(bAndNotC);
  }
}
```
